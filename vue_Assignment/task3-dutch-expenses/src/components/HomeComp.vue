<template>
  <div>
    <h2 class="mb-3">Group Members</h2>
    <div class="input-group mb-3">
      <input v-model="newMember" type="text" class="form-control form-control-sm" placeholder="Enter name" />
      <button class="btn btn-primary btn-sm" @click="addMember">Add</button>
    </div>
    <ul class="list-group mb-3">
      <li class="list-group-item d-flex justify-content-between align-items-center" v-for="(member, index) in members" :key="index">
        {{ member }}
        <button class="btn btn-danger btn-sm" @click="removeMember(index)">Remove</button>
      </li>
    </ul>
    <button class="btn btn-success" @click="$emit('go-to-expense')">Go to Expenses</button>
  </div>
</template>

<script>
export default {
  props: ['members'],
  data() {
    return { newMember: '' };
  },
  methods: {
    addMember() {
      if (this.newMember.trim()) {
        this.$emit('update-members', [...this.members, this.newMember.trim()]);
        this.newMember = '';
      }
    },
    removeMember(index) {
      const updated = [...this.members];
      updated.splice(index, 1);
      this.$emit('update-members', updated);
    }
  }
};
</script>