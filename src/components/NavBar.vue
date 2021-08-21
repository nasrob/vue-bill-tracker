<template>
	<ul class="list-none flex justify-center border-b-4 mb-0">
		<li
			class="top-menu-item"
			v-for="category in categories"
			:key="category"
		>
			{{ category }}
		</li>
		<li class="top-menu-item" @click="triggerShowAddCategory">
			➕
		</li>
	</ul>
</template>

<script>
export default {
	props: ["categories"],
	methods: {
		triggerShowAddCategory() {
			this.$emit("triggerShowAddCategory");
		},
	},
};
</script>

<style scoped>
.top-menu-item {
	@apply p-4 inline bg-gray-200 hover:bg-gray-400 uppercase font-black cursor-pointer;
}
</style>
