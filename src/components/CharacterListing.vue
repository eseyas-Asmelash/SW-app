<template>
  <div class="container">

    <character-listing-item
      v-for="character in characters"
      v-bind:key="character.id"
      class="box"
      v-bind:character="character"
      v-on:toggle-active-character="
        event => $emit('toggle-active-character', event)
      "
    >
    </character-listing-item>
  </div>
</template>

<script>
import CharacterListingItem from "./CharacterListingItem.vue";

export default {
  name: "CharacterListing",

  props: {
    characters: {
      type: Array,
      required: true,
      default: () => []
    }
  },

  components: {
    CharacterListingItem
  }
};
</script>
