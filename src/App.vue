<script setup>
import PersonTable from "./components/PersonTable.vue";
import PersonFilter from "./components/PersonFilter.vue";
</script>

<template>
  <div class="container">
    <main class="container">
      <PersonFilter @searching="charSearch" />
      <PersonTable :characterName="characterSearch" />
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      characterSearch: "",
    };
  },
  methods: {
    charSearch(data) {
      this.characterSearch = data
    }
  },
};
</script>
