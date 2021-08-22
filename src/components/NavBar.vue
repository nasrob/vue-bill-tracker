<template>
	<ul class="list-none flex justify-center border-b-4 mb-0">
		<li
			class="top-menu-item"
			:class="[activeCategory === '' ? 'bg-gray-600' : 'bg-gray-200']"
			@click="clearActiveCategory()"
		>
			All
		</li>
		<li
			class="top-menu-item"
			:class="[
				activeCategory === category ? 'bg-gray-600' : 'bg-gray-200',
			]"
			v-for="category in categories"
			:key="category"
			@click="setActiveCategory(category)"
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
	props: ["categories", "activeCategory"],
	methods: {
		triggerShowAddCategory() {
			this.$emit("triggerShowAddCategory");
		},
		clearActiveCategory() {
			this.$emit("clearActiveCategory");
		},
		setActiveCategory(category) {
			this.$emit("setActiveCategory", category);
		},
	},
};
</script>

<style scoped>
.top-menu-item {
	@apply p-4 inline hover:bg-gray-400 uppercase font-black cursor-pointer;
}
</style>
