<template>
  <div class="more-wrapper">
      <div class="more-head">
        <btn back/>
        <btn more @click.native="moreClicked"/>
      </div>
    <div class="more-body">
    <img :src="artworkPath" class="more-cover"/>
    <div class="now-playing">
      <span class="song">{{song}}</span>
      <span class="artist">{{artist}}</span>
    </div>
      <span class="divider">...</span>
      <div class="options">
        <p class="option">Add to playlist</p>
        <p class="option">Show album</p>
        <p class="option">Share with friends</p>
      </div>

    </div>
  </div>
</template>

<script>
import Btn from './Btn'
export default {
  components: {
    Btn
  },
  props: {
    song: {
      type: String
    },
    artist: {
      type: String
    },
    artworkPath: {
      type: String
    }
  },
  methods: {
    moreClicked() {
      this.$emit('return');
      console.log('more clicked in more!')
    }
  }
}
</script>

<style scoped lang="scss">
.more-wrapper {
  width: 576px;
  height: calc(1024px - 89px);
  position: absolute;
  z-index: 2;
  color: white;
  background-color: rgba(20, 20, 20, 0.9);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-content: space-around;
  align-items: center;
  text-align: center;
  z-index: 3;
  .more-cover {
    max-height: 30%;
    margin-bottom: 3rem;
  }
  .now-playing {
    display: flex;
    flex-direction: column;
    align-items: center;
    .song {
      font-size: 36px;
      line-height: 36px;
      color: #37b34a;
      font-family: "Source Sans Pro";
      text-align: center;
    }
    .artist {
      font-size: 18px;
      line-height: 36px;
      color: #9a9b9b;
      font-family: "Source Sans Pro";
      text-align: center;
      text-transform: uppercase;
    }
  }
  .divider {
    letter-spacing: 1rem;
    margin-top: 1rem;
    display: flex;
  }
  .options {
    font-size: 24px;
    line-height: 64px;
    color: #ffffff;
    font-family: "Source Sans Pro";
  }
}
.more-head {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 8.1rem;
  justify-content: space-between;
}
.more-body {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  p {
    line-height: 3rem;
  }
}
</style>
