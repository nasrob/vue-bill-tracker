<template>
	<div
		class="h-100 w-full flex items-center justify-center font-sans"
	>
		<div
			class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg"
		>
			<div class="mb-4">
				<h1 class="text-gray-800">Enter a category of bills</h1>
				<p>E.g. 'Electricity' or 'Gas' or 'Internet'</p>
				<div class="flex">
					<input
						placeholder="Add a category"
						v-model="category"
						class="shadow appearance-none border rounded w-full py-2 mr-4 text-gray-700"
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
	</div>
</template>

<script>
export default {
	name: "AddCategory",
	data: function() {
		return {
			category: "",
		};
	},
	methods: {
		handleClick: function() {
			if (!this.category) {
				alert("Enter a category");
				return;
			}
			this.$emit("addCategory", this.category);
		},
	},
};
</script>

<style></style>
