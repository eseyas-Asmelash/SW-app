<template>
  <div class="home">
    <h1 class="title has-text-info">Star Wars Characters</h1>
    <div class="container p-5">
      <div class="column_wrapper">
        <character-listing class=""
          v-bind:characters="characters"
          v-on:toggle-active-character="onToggleActiveCharacter"
        ></character-listing>
      </div>
      </div>
  </div>
</template>

<script>
import CharacterListing from "@/components/CharacterListing.vue";
import axios from "axios";

export default {
  name: "Home",

  data() {
    return {
      characters: []
    };
  },

  components: {
    CharacterListing
  },

  async created() {
    this.characters = await this.getCaratteri();
  },

  methods: {
    onToggleActiveCharacter(character) {
      const index = this.characters.findIndex(
        localCharacter => localCharacter.id === character.id
      );

      if (index >= 0) {
        const updatedCharacter = {
          ...character,
          active: !character.active
        };
        this.characters.splice(index, 1, updatedCharacter);
      }
    },
    getCaratteri() {
      let caratteri = [];
      for(var i = 1; i < 100; i++) {
        axios.get('https://swapi.dev/api/people/' + i + '/')
        .then(response => {
          caratteri.push(response.data);
          console.log(response.data);
        })
      }
      return caratteri;
    }
  }
};
</script>
<style>
.column_wrapper {
  column-count: 2;
}

</style>
