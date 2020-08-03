<template>
  <div class="emoji-container">
    <header class="header">
      <h2>Emoji Search</h2>
    </header>
    <app-search-emoji></app-search-emoji>
    <app-loader v-if="loading === true"></app-loader>
    <app-emoji-container :emojis="emojis"></app-emoji-container>
  </div>
</template>

<script>
import axios from 'axios';
import SearchEmoji from './SearchInput';
import EmojiContainer from './EmojiContainer';
import Loader from './Loader';

export default {
  data() {
    return {
      emojis: [],
      loading: true
    };
  },
  created() {
    axios
      .get(
        'https://emoji-api.com/emojis?access_key=98ee116c8a0103940362af590ec9388d03de4851'
      )
      .then(response => {
        let data = '';
        for (let i = 0; i < response.data.length; i++) {
          data = response.data[i];
          this.emojis.push(data);
          this.loading = false;
        }
      })
      .catch(err => console.log(err));
  },
  components: {
    appSearchEmoji: SearchEmoji,
    appEmojiContainer: EmojiContainer,
    appLoader: Loader
  }
};
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: center;
  padding: 1rem;
  font-size: 2rem;
}
</style>
