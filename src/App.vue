/* eslint-disable vue/valid-v-else */
<template>
	<main>
		<AddCategory
			v-if="shouldShowAddCategory"
			v-on:addCategory="addCategory($event)"
		/>
		<div v-else-if="shouldShowAddBill">
			<AddBill
				:categories="categories"
				v-on:addBill="addBill($event)"
			/>
		</div>
		<div v-else>
			<NavBar
				:categories="categories"
				:activeCategory="activeCategory"
				v-on:triggerShowAddCategory="triggerShowAddCategory"
				v-on:clearActiveCategory="clearActiveCategory"
				v-on:setActiveCategory="setActiveCategory"
			/>
			<div class="container flex">
				<div class="w-1/2">
					<BillsTable
						:bills="activeBills"
						v-on:triggerShowAddBill="triggerShowAddBill"
						v-on:removeBill="removeBill()"
					/>
				</div>
				<div class="w-1/2">
					<Chart :bills="activeBills" />
				</div>
			</div>
		</div>
	</main>
</template>

<script>
import AddCategory from "./components/AddCategory.vue";
import AddBill from "./components/AddBill.vue";
import NavBar from "./components/NavBar.vue";
import Chart from "./components/Chart.vue";
import BillsTable from "./components/BillsTable.vue";

export default {
	/* eslint-disable */
	name: "App",
	components: {
		AddCategory,
		AddBill,
		Chart,
		BillsTable,
		NavBar,
	},
	data() {
		return {
			bills: [],
			categories: [],
			shouldShowAddCategory: true,
			shouldShowAddBill: true,
			activeCategory: "",
		};
	},
	methods: {
		addCategory(category) {
			this.categories.push(category);
			this.shouldShowAddCategory = false;
		},
		triggerShowAddCategory() {
			this.shouldShowAddCategory = true;
		},
		addBill(bill) {
			this.bills.push(bill);
			this.shouldShowAddBill = false;
		},
		triggerShowAddBill() {
			this.shouldShowAddBill = true;
		},
		removeBill(index) {
			this.bills = this.bills
				.slice(0, index)
				.concat(this.bills.slice(index + 1, this.bills.length));
		},
		clearActiveCategory() {
			this.activeCategory = "";
		},
		setActiveCategory(category) {
			this.activeCategory = category;
		},
	},
	watch: {
		categories() {
			localStorage.setItem(
				"categories",
				JSON.stringify(this.categories)
			);
		},
		bills() {
			localStorage.setItem("bills", JSON.stringify(this.bills));
		},
	},
	mounted() {
		if (localStorage.getItem("categories")) {
			this.categories = JSON.parse(
				localStorage.getItem("categories")
			);
		}

		if (!this.categories.length) {
			this.shouldShowAddCategory = true;
		}

		if (localStorage.getItem("bills")) {
			this.bills = JSON.parse(localStorage.getItem("bills"));
		}
	},
	computed: {
		activeBills() {
			return this.bills
				.filter((bill) =>
					this.activeCategory
						? bill.category === this.activeCategory
						: true
				)
				.sort((a, b) =>
					new Date(a.date) < new Date(b.date) ? 1 : -1
				);
		},
	},
};
</script>

<style></style>
