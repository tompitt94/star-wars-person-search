<script setup>
import PersonTable from "./components/PersonTable.vue";
import PersonFilter from "./components/PersonFilter.vue";
</script>

<template>
  <div>
    <main class="container">
      <div class="block">
        <PersonFilter @searching="charSearch" />
      </div>
      <div class="block">
        <PersonTable :characterName="characterSearch" />
      </div>
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
      // Updates characterSearch which is passed to the personTable component via prop
      this.characterSearch = data;
    },
  },
};
</script>
