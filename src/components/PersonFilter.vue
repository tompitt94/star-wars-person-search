<!-- Component to allow the user to type the name of the character they wish to find -->

<template>
  <div class="columns mt-4">
    <div class="column is-half">
      <input
        class="input"
        type="text"
        placeholder="Use the force....to search by the characters name"
        v-model="name"
        @keyup="search"
      />
    </div>
  </div>
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
      // Emits event to app.vue and passes the current name that has been typed - updates on every key press
      this.$emit("searching", this.name);
    },
  },
};
</script>

<style></style>
