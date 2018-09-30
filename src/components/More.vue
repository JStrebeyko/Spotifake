<template>
  <div class="more-wrapper">
      <div class="more-head">
        <btn back/>
        <btn moreMore @click.native="moreClicked"/>
      </div>
    <div class="more-body">
    <img :src="artworkPath" class="more-cover"/>
    <div class="now-playing">
      <span class="song">{{song}}</span>
      <span class="artist">{{artist}}</span>
    </div>
      <span class="divider">...</span>
      <div class="options">
        <span class="option" @click="add">Add to playlist</span>
        <span class="option">Show album</span>
        <span class="option">Share with friends</span>
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
    },
    add() {
      console.log(`"${this.song}" by ${this.artist} has been added to playlist!`)
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
  background-color: rgba(27, 27, 27, 0.96);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: space-around;
  align-items: center;
  text-align: center;
  z-index: 3;
  .more-head {
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 8.1rem;
    justify-content: space-between;
    .btn {
      margin-top: 1.3rem;
    }
    .btn-more {
      fill: white;
    }
  }
  .more-body {
    margin-bottom: 4rem;
    .more-cover {
      height: 25%;
      margin-bottom: 1.5rem;
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
      letter-spacing: 0.4rem;
      margin-left: 0.4rem;
      font-size: 2rem;
      color: #9a9b9b;
    }
    .options {
      display: flex;
      flex-direction: column;
      padding-top: 1rem;
      font-size: 24px;
      line-height: 64px;
      color: #ffffff;
      font-family: "Source Sans Pro";
      .option {
        cursor: pointer;
        &:hover {
          text-shadow: 1px 1px 2px white,
                       -1px -1px 2px white
        }
      }
    }
  }
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
