<template>
	<table class="table">
		<thead class="bg-blue-400 text-white">
			<tr>
				<th class="w-1/3 mx-3" scope="col">Date</th>
				<th class="w-1/3 mx-3" scope="col">Amount</th>
				<th class="w-1/3 mx-3" scope="col">Category</th>
				<th scope="col"></th>
			</tr>
		</thead>
		<tbody>
			<tr class="p-4 bg-blue-200 text-center">
				<td colspan="4">
					<button class="underline" @click="triggerShowAddBill">
						Add new
					</button>
				</td>
			</tr>

			<tr
				v-for="(bill, index) in bills"
				:key="index"
				class="p-4 text-center"
			>
				<td class="w-1/4 mx-3">
					{{ moment(bill.date).format("MM DD YYYY") }}
				</td>
				<td class="w-1/4 mx-3">{{ bill.amount }}</td>
				<td class="w-1/4 mx-3">{{ bill.category }}</td>
				<td class="w-1/4">
					<button @click="removeBill(index)">𝗫</button>
				</td>
			</tr>
		</tbody>
	</table>
</template>

<script>
import moment from "moment";

export default {
	name: "BillsTable",
	props: ["bills"],
	methods: {
		triggerShowAddBill() {
			this.$emit("triggerShowAddBill");
		},
		removeBill(index) {
			this.$emit("removeBill", index);
		},
	},
	created() {
		this.moment = moment;
	},
};
</script>

<style></style>
