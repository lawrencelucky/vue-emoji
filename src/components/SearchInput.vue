<template>
  <div class="search-input-container">
    <input
      class="search-input"
      type="text"
      placeholder="Search for Emojis..."
      @keyup="searchedText"
    />
    <app-loader v-if="loading === true"></app-loader>
  </div>
</template>

<script>
import axios from 'axios';
import { eventBus } from '../main';
import Loader from './Loader';

export default {
  data() {
    return {
      emoji: '',
      searchResult: '',
      loading: null
    };
  },
  methods: {
    searchedText(event) {
      const value = event.target.value;
      this.emoji = value;
      this.loading = true;
      axios
        .get(
          `https://emoji-api.com/emojis?search=${this.emoji}&access_key=98ee116c8a0103940362af590ec9388d03de4851`
        )
        .then(response => {
          this.searchResult = response.data;
          eventBus.$emit('searchMade', this.searchResult);
          this.loading = false;
        })
        .catch(err => console.log(err));
    }
  },
  components: {
    appLoader: Loader
  }
};
</script>

<style lang="scss" scoped>
.search-input-container {
  display: flex;
  flex-flow: column;
  align-items: center;
  margin: 3rem 0;

  .search-input {
    width: 60vw;
    padding: 1rem;
    border: 3px solid #b388ff;
    border-radius: 10px;
    font-size: 1.6rem;
    transition: all 0.5s;

    &::placeholder {
      color: #bdbdbd;
    }

    &:focus {
      outline: 0;
      border-color: #303f9f;
    }
  }
}
</style>
