<template>
  <div class="box">
    <div class="columns">
      <div class="column">
        <h3 class="title is-3">
          <span>{{ character.name }}</span>
        </h3>
      </div>

<!--       <div class="column is-narrow">
        <button
          class="button"
          v-bind:class="{
            'is-danger': character.active,
            'is-success': !character.active,
          }"
          v-on:click="onClickToggleActive"
        >
          {{ toggleActiveButtonText }}
        </button>
      </div> -->
    </div>

    <button
      class="button is-small is-fullwidth"
      v-on:click="onClickToggleDetails"
    >
      {{ toggleDetailsButtonText }}
    </button>

    <div class="content" v-if="visible">
      <p>{{ character.description }}</p>
      <p>Height: {{ character.height }}</p>
      <p>Mass: {{ character.sass }}</p>
      <p>Birth_year: {{ character.birth_year }}</p>
      <p>Gender: {{ character.gender }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CharacterListingItem",

  data() {
    return {
      visible: false,
    };
  },

  props: {
    character: {
      type: Object,
      required: true,
      default: () => {},
    },
  },

  computed: {
    toggleDetailsButtonText() {
      return this.visible ? "Hide details" : "View details";
    },
    toggleActiveButtonText() {
      return this.character.active ? "Deactivate" : "Activate";
    },
  },

  methods: {
    onClickToggleDetails(event) {
      console.log(event);
      this.visible = !this.visible;
    },
    onClickToggleActive() {
      this.$emit("toggle-active-character", this.character);
    }
  },
};
</script>
