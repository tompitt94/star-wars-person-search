<script setup>
defineProps({
  tableData: {
    type: Object,
    required: true,
  },
  characterName: {
    type: String,
    required: false,
  },
});
</script>

<template>
  <div>
    <table class="table is-hoverable is-fullwidth">
      <thead>
        <tr>
          <th v-for="col in tableColumns" :key="col">{{ col }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="person in filteredCharacters" :key="person.name">
          <td>{{ person.name }}</td>
          <td>{{ person.height }}cm</td>
          <td>{{ person.mass }}Kg</td>
          <td>{{ new Date(person.created).toLocaleDateString("en-GB") }}</td>
          <td>{{ new Date(person.edited).toLocaleDateString("en-GB") }}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
    <nav class="pagination is-rounded" role="navigation" aria-label="pagination">
      <ul class="pagination-list">
        <li><a class="pagination-link" aria-label="Goto page 1">1</a></li>
        <li><span class="pagination-ellipsis">&hellip;</span></li>
        <li><a class="pagination-link" aria-label="Goto page 45">45</a></li>
        <li><a class="pagination-link is-current" aria-label="Page 46" aria-current="page">46</a></li>
        <li><a class="pagination-link" aria-label="Goto page 47">47</a></li>
        <li><span class="pagination-ellipsis">&hellip;</span></li>
        <li><a class="pagination-link" aria-label="Goto page 86">86</a></li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableColumns: [
        "Name",
        "Height",
        "Mass",
        "Created",
        "Edited",
        "Planet Name",
      ],
      people: []
    };
  },
  computed: {
    filteredCharacters() {
      if (!this.characterName) {
        return this.people;
      } else {
        return this.people.filter((character) =>
          character.name
            .toLowerCase()
            .includes(this.characterName.toLowerCase())
        );
      }
    },
  },
  mounted() {
    fetch("https://swapi.dev/api/people/")
      .then((response) => response.json())
      .then((data) => (this.people = data.results));
  },
};
</script>
