<template>
  <div class="card">
    <h1>Search</h1>
    <form @submit="updateJokesForm">
      <input
        type="text"
        placeholder="Search the jokes"
        v-model="jokeQuery"
        v-on:keypress="isLetter($event)"
        @keypress.enter="updateJokesForm"
        id="search"
        name="search"
        required
        aria-label="Search"
      />
      <button type="submit">Submit</button>
    </form>
    <p v-if="!jokes">Loading...</p>
    <p v-else-if="!jokes.length">No jokes found</p>
    <ol v-else>
      <li v-for="(joke, index) in jokes" :index="index">
        {{ joke.joke }}
      </li>
    </ol>
    
  </div>
</template>

<script lang="ts">
import { ref } from "vue";

export default {
  name: "SearchPage",
  setup() {
    const jokes = ref(null);
    const jokeQuery = ref("");

    async function updateJokes() {
      jokes.value = null;
      const res = await fetch(
        `https://icanhazdadjoke.com/search?term=${jokeQuery.value}&limit=10`,
        {
          headers: {
            accept: "application/json",
          },
        }
      );
      const data = await res.json();
      jokes.value = data.results;
    }

    updateJokes();

    async function updateJokesForm(e: { preventDefault: () => void; }) {
      e.preventDefault();
      await updateJokes();
    }

    return { jokes, jokeQuery, updateJokesForm };
  },
  methods: {
    isLetter(e: KeyboardEvent) {
      const char = String.fromCharCode(e.keyCode);
      if (/^[A-Za-z]+$/.test(char)) return true;
      else e.preventDefault();
    },
  },
};
</script>
