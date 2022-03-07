<!-- Component to retrieve the character data and display in a table format -->
<script setup>
defineProps({
  //This will be used to filter the results displayed in the table if the user begins to type a character name
  characterName: {
    type: String,
    required: false,
  },
});
</script>

<template>
  <div class="table-container mb-5">
    <table class="table is-hoverable is-fullwidth">
      <thead>
        <tr>
          <th v-for="col in tableColumns" :key="col">{{ col }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-if="filteredCharacters.length === 0">
          <td>The Force has not provided any results</td>
        </tr>
        <!-- Using v-for to loop through filteredCharacters to avoid hard coding data -->
        <tr v-for="person in filteredCharacters" :key="person.name">
          <td>{{ person.name }}</td>
          <td>
            {{ person.height }}
            <!--Included conditional unit in case of unknown data-->
            <span v-if="person.height !== 'unknown'">cm</span>
          </td>
          <td>
            {{ person.mass }}
            <!--Included conditional unit in case of unknown data-->
            <span v-if="person.mass !== 'unknown'">Kg</span>
          </td>
          <td>
            <!--Transforming date into readable and familiar formats-->
            {{ new Date(person.created).toLocaleDateString("en-GB") }}
          </td>
          <td>
            <!--Transforming date into readable and familiar formats-->
            {{ new Date(person.edited).toLocaleDateString("en-GB") }}
          </td>
          <td>
            <!-- Comparing planets Object Array for Planet URL and Homeworld URL -->
            {{
              this.planets.find((planet) => planet.url == person.homeworld).name
            }}
          </td>
        </tr>
      </tbody>
    </table>
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
        "Home Planet",
      ],
      characters: [], // Will be populated on Mount and have all characters pushed into it
      planets: [],
    };
  },
  methods: {
    // Function to reun through the SWAPI endpoints
    async fetchApiResults(url, array) {
      // Setting the first page to be called
      let page = 1;
      // Using this to check if there is a next page to end
      let lastResult = [];

      do {
        try {
          const resp = await fetch(`${url}${page}`);
          const data = await resp.json();
          lastResult = data;
          // pushing data to create one large array
          data.results.forEach((item) => {
            array.push(item);
          });
          // Increment API page number
          page++;
        } catch (err) {
          console.error(`The force is not strong right now - ${err}`);
        }
        // Keep going until no "next" page is provided
      } while (lastResult.next !== null);
    },
  },
  computed: {
    filteredCharacters() {
      // Return full list of characters if no search terms are provided by the user
      if (!this.characterName) {
        return this.characters;
      } else {
        // Check for any character names that contain the search terms provided by the user
        return this.characters.filter((character) =>
          character.name
            .toLowerCase()
            .includes(this.characterName.toLowerCase())
        );
      }
    },
  },
  async mounted() {
    this.fetchApiResults(
      "https://swapi.dev/api/people/?page=",
      this.characters
    );

    this.fetchApiResults("https://swapi.dev/api/planets/?page=", this.planets);
  },
};
</script>
