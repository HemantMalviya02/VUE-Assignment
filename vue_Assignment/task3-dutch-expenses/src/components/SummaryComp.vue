<!-- SummaryComp.vue -->
<template>
  <div>
    <h2 class="mb-4">Summary</h2>
    <ul class="list-group">
      <li class="list-group-item" v-for="(line, index) in results" :key="index">{{ line }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['members', 'expenses'],
  computed: {
    balances() {
      const balances = {};
      this.members.forEach(m => balances[m] = 0);

      this.expenses.forEach(e => {
        const perHead = e.amount / this.members.length;

        this.members.forEach(m => balances[m] -= perHead);
        e.payers.forEach(p => balances[p.name] += p.amount);
      });

      return balances;
    },
    results() {
      const creditors = [], debtors = [], lines = [];
      for (const [name, amount] of Object.entries(this.balances)) {
        if (amount > 0) creditors.push({ name, amount });
        else if (amount < 0) debtors.push({ name, amount: -amount });
      }

      creditors.sort((a, b) => b.amount - a.amount);
      debtors.sort((a, b) => b.amount - a.amount);

      while (creditors.length && debtors.length) {
        let creditor = creditors[0];
        let debtor = debtors[0];
        let amount = Math.min(creditor.amount, debtor.amount);

        lines.push(`${debtor.name} owes ₹${amount.toFixed(2)} to ${creditor.name}`);

        creditor.amount -= amount;
        debtor.amount -= amount;

        if (creditor.amount === 0) creditors.shift();
        if (debtor.amount === 0) debtors.shift();
      }

      return lines;
    }
  }
};
</script>