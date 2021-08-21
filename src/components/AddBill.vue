<template>
	<div
		class="h-100 w-full flex items-center justify-center font-sans"
	>
		<div
			class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg"
		>
			<h1 class="text-gray-800">Enter a new Bill</h1>
			<p></p>
			<div class="flex mt-4">
				<datepicker
					class="shadow appearance-none border rounded text-gray-700 w-full py-2 px-3 mr-4"
					v-model="date"
				/>

				<select v-model="category" class="mx-3">
					<option
						v-for="category of categories"
						:value="category"
						:key="category"
						>{{ category }}</option
					>
				</select>

				<input
					class="form-item"
					placeholder="Set an Amount"
					v-model="amount"
				/>
				<button
					class="flex-shrink-0 p-2 border-2 rounded bg-green-400 hover:text-white hover:bg-green-700"
					@click="handleClick"
				>
					Add
				</button>
			</div>
		</div>
	</div>
</template>

<script>
import Datepicker from "vue3-datepicker";

export default {
	name: "AddBill",
	components: { Datepicker },
	props: ["categories"],
	emits: ["addBill"],
	data() {
		return {
			date: new Date(),
			category: this.categories[0],
			amount: 0,
		};
	},
	methods: {
		handleClick: function() {
			if (!this.date) {
				alert("Enter a Date");
				return;
			}

			if (!this.amount) {
				alert("Enter an amount");
				return;
			}

			this.$emit("addBill", {
				date: this.date,
				category: this.category,
				amount: parseInt(this.amount, 10),
			});
		},
	},
};
</script>

<style scoped>
.form-item {
	@apply shadow appearance-none border rounded text-gray-700 w-full py-2 px-3 mr-4;
}
</style>
