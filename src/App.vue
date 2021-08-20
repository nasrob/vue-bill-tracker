<template>
	<main>
		<NavBar />
		<div class="container flex">
			<BillsTable />
		</div>
		<div class="w-1/2">
			<Char :bills="activeBills" />
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
	name: "App",
	components: {
		AddCategory,
		AddBill,
		Chart,
		BillsTable,
		NavBar,
	},
};
</script>

<style></style>
