<template>
  <div v-if="canShow" class="mb-8">
    <table class="table-fixed w-full">
      <thead class="bg-whitesmoke">
        <tr>
          <th class="one-fifth font-medium">Amount</th>
          <th class="two-fifth font-medium">TXid</th>
          <th class="one-fifth font-medium">Status</th>
          <th class="one-fifth font-medium">Date</th>
        </tr>
      </thead>
      <tbody v-if="!loading">
        <tr
          v-for="transaction of transactions"
          :key="transaction.id"
          class="cursor-pointer"
        >
          <td class="text-lg">{{ transaction.amount | naira }}</td>
          <td class="text-secondary text-sm underline">{{ transaction.payment_link_id }}</td>
          <td class="text-sm"><Status :status="transaction.status" /></td>
          <td class="text-lg">{{ transaction.created_at | dateString }}</td>
        </tr>
      </tbody>
    </table>
    <PaginationLoader v-if="loading" class="mt-6" />
  </div>
</template>

<script>
import Status from "./Status.vue";

export default {
  name: 'Table',
  components: {
    Status,
  },
  props: {
    transactions: {
      type: Array,
      default: () => []
    },
    loading: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    canShow(){
      return this.loading || this.transactions.length
    }
  }
}
</script>

<style lang="css" scoped>
  .one-fifth{
    width: 20%;
  }

  .two-fifth{
    width: 40%;
  }
</style>