<template>
  <div class="container py-4" style="max-width: 600px;">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark mb-4">
      <div class="container-fluid">
        <span class="navbar-brand text-white">Dutch App</span>
        <div class="navbar-nav">
          <button class="nav-link btn btn-link text-white" :class="{ 'border border-white': currentScreen === 'home' }" @click="currentScreen = 'home'">Home</button>
          <button class="nav-link btn btn-link text-white" :class="{ 'border border-white': currentScreen === 'expenses' }" @click="currentScreen = 'expenses'">Expenses</button>
          <button class="nav-link btn btn-link text-white" :class="{ 'border border-white': currentScreen === 'summary' }" @click="currentScreen = 'summary'">Summary</button>
        </div>
      </div>
    </nav>

    <HomeComp
      v-if="currentScreen === 'home'"
      :members="members"
      @update-members="members = $event"
      @go-to-expense="currentScreen = 'expenses'"
    />

    <ExpenseComp
      v-if="currentScreen === 'expenses'"
      :members="members"
      :expenses="expenses"
      @add-expense="handleAddExpense"
    />

    <SummaryComp
      v-if="currentScreen === 'summary'"
      :members="members"
      :expenses="expenses"
    />
  </div>
</template>

<script>
import HomeComp from './components/HomeComp.vue';
import ExpenseComp from './components/ExpenseComp.vue';
import SummaryComp from './components/SummaryComp.vue';

export default {
  components: { HomeComp, ExpenseComp, SummaryComp },
  data() {
    return {
      currentScreen: 'home',
      members: [],
      expenses: []
    };
  },
  methods: {
    handleAddExpense(expense) {
      this.expenses.push(expense);
      this.currentScreen = 'summary';
    }
  }
};
</script>