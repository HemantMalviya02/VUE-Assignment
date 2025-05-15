<template>
  <div>
    <h2 class="mb-3">Add Expense</h2>

    <div class="mb-3">
      <input v-model.number="amount" type="number" class="form-control form-control-sm" placeholder="Total Amount" />
    </div>

    <div class="mb-3">
      <h5>Select Payers:</h5>
      <div v-for="member in members" :key="member" class="input-group input-group-sm mb-1">
        <div class="input-group-text">
          <input type="checkbox" v-model="selectedPayers[member]" />
        </div>
        <span class="input-group-text w-50">{{ member }}</span>
        <input type="number" v-model.number="payerAmounts[member]" :disabled="!selectedPayers[member]" class="form-control form-control-sm" placeholder="Amount paid" />
      </div>
    </div>

    <div v-if="error" class="alert alert-danger">{{ error }}</div>

    <button class="btn btn-primary" @click="saveExpense">Save Expense</button>
  </div>
</template>

<script>
export default {
  props: ['members'],
  data() {
    return {
      amount: 0,
      selectedPayers: {},
      payerAmounts: {},
      error: ''
    };
  },
  methods: {
    saveExpense() {
      const payers = Object.entries(this.selectedPayers)
        .filter(([name, selected]) => selected)
        .map(([name]) => ({ name, amount: this.payerAmounts[name] || 0 }));

      const totalPaid = payers.reduce((sum, p) => sum + p.amount, 0);

      if (totalPaid !== this.amount) {
        this.error = `Total paid (₹${totalPaid}) does not match the total amount (₹${this.amount})`;
        return;
      }

      this.error = '';
      this.$emit('add-expense', { amount: this.amount, payers });

      // Reset form
      this.amount = 0;
      this.selectedPayers = {};
      this.payerAmounts = {};
    }
  }
};
</script>