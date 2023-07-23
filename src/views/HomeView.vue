<template>
  <div>
    <h1>Really bad jokes..</h1>
    <joke-single :text="joke"></joke-single>
    <button @click="getDadJoke">New Joke</button>
  </div>
</template>

<script lang="ts">
import JokeSingle from "@/components/JokeSingle.vue";

export default {
  name: "HomePage",
  components: {
    JokeSingle,
  },
  data() {
    return {
      joke: "",
    };
  },
  methods: {
    async getDadJoke() {
      const response = await fetch("https://icanhazdadjoke.com/", {
        headers: {
          Accept: "application/json",
        },
      });
      const json = await response.json();
      this.joke = json.joke;
    },
  },
  mounted() {
    this.getDadJoke();
  },
};
</script>
