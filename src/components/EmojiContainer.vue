<template>
  <div class="emoji-container">
    <template v-if="searchText === ''">
      <div class="emoji">
        <li class="emoji-list" v-for="(emoji, index) in character" :key="index">
          <p class="emoji-icon">{{ emoji.character }}</p>
          <p class="emoji-title">{{ emoji.unicodeName }}</p>
        </li>
      </div>
    </template>
    <template v-else-if="searchText !== ''">
      <div class="emoji">
        <li
          class="emoji-list"
          v-for="(emoji, index) in searchText"
          :key="index"
        >
          <p class="emoji-icon">{{ emoji.character }}</p>
          <p class="emoji-title">{{ emoji.unicodeName }}</p>
        </li>
      </div>
    </template>
  </div>
</template>

<script>
import { eventBus } from '../main';

export default {
  props: ['emojis'],
  data() {
    return {
      character: '',
      searchText: ''
    };
  },
  created() {
    this.character = this.emojis;
    eventBus.$on('searchMade', searchedResult => {
      this.searchText = searchedResult;
    });
  }
};
</script>

<style lang="scss" scoped>
.emoji-container {
  display: flex;
  justify-content: center;

  .emoji {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    justify-items: center;
    align-items: center;
    grid-gap: 1rem;
    transition: all 0.3s;

    .emoji-list {
      list-style: none;
      display: flex;
      flex-flow: column;
      border: 2px solid #b388ff;
      border-radius: 10px;
      padding: 2rem;
      cursor: pointer;

      .emoji-icon {
        font-size: 4rem;
        text-align: center;
        margin-bottom: 2rem;
        transition: all 0.3s;

        &:hover {
          transform: scale(1.1);
        }
      }

      .emoji-title {
        font-size: 1rem;
        width: 8rem;
        text-align: center;
      }
    }
  }
}
</style>
