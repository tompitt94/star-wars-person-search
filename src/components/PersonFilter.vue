<template>
  <input
    class="input"
    type="text"
    placeholder="Search by Name"
    v-model="name"
    @keyup="search"
  />
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },
  methods: {
    search() {
      this.$emit("searching", this.name);
    },
  },
};
</script>

<style></style>
