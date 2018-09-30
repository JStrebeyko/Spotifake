<template>
    <button :class="className">
      <img v-if="back" src="./../assets/back_ico.svg"/>
      <img v-if="more" src="./../assets/more_ico.svg"/>
      <img v-if="shuffle" src="./../assets/shuffle_ico.svg"/>
      <img v-if="prev" src="./../assets/previous_ico.svg"/>
      <img v-if="next" src="./../assets/next_ico.svg"/>
      <img v-if="repeat" src="./../assets/repeat_ico.svg"/>
      <img v-if="playlist" src="./../assets/playlist_ico.svg"/>
      <img v-if="play && active" src="./../assets/Play_active.png"/>
      <img v-if="play && !active" src="./../assets/Play_inactive.png"/>
      <img v-if="down" src="./../assets/back_ico.svg"/>
      <span v-if="shufflePlay" class="shuffle-play-text">shuffle play</span>
      <svg  v-if="moreMore" width="4" height="29" viewBox="0 0 4 29">
  <path id="more_ico" fill="white" d="M1023,163.031a1.985,1.985,0,1,1-2,1.985A2,2,0,0,1,1023,163.031Zm0-12.531a2,2,0,1,1-2,2A2,2,0,0,1,1023,150.5Zm0-12.5a1.985,1.985,0,1,1-2,1.984A1.995,1.995,0,0,1,1023,138Z" transform="translate(-1021 -138)"/>
</svg>
    </button>
</template>

<script>
export default {
  data() {
    return {
      src: ''
    }
  },
  props: {
    more: {
      type: Boolean
    },
    back: {
      type: Boolean
    },
    shuffle: {
      type: Boolean
    },
    prev: {
      type: Boolean
    },
    play: {
      type: Boolean
    },
    active: {
      type: Boolean
    },
    next: {
      type: Boolean
    },
    repeat: {
      type: Boolean
    },
    playlist: {
      type: Boolean
    },
    down: {
      type: Boolean
    },
    shufflePlay: {
      type: Boolean
    },
    active: {
      type: Boolean
    },
    moreMore: {
      type: Boolean
    }
  },
  mounted() {

  },
  computed: {
    className() {
      let className;
      this.back && (className = 'btn btn-back');
      (this.more||this.moreMore) && (className = 'btn btn-more');
      this.shuffle && (className = 'btn btn-shuffle');
      this.prev && (className = 'btn btn-prev');
      this.play && (className = 'btn btn-play');
      this.next && (className = 'btn btn-next');
      this.repeat && (className = 'btn btn-repeat');
      this.playlist && (className = 'btn btn-playlist');
      this.down && (className = 'btn btn-down');
      this.shufflePlay && (className = 'btn btn-shuffle-play');
      return className;
    }
  }
}
</script>

<style scoped lang="scss">
button, input[type="submit"], input[type="reset"] {
  background: none;
  color: inherit;
  border: none;
  padding: 0;
  font: inherit;
  cursor: pointer;
  outline: inherit;
 z-index: 2;
}

.btn-back, .btn-more {
 display: flex;
 justify-content: center;
}
.btn-back {
 img {
    margin-left: 3.3rem;
    margin-top: 0.4rem;
  }
}
.btn-more img,
.btn-more svg {
    margin-right: 3.9rem;
    margin-top: 0.4rem;
}

.btn-play {
  max-width:13rem;
  display: flex;
  margin-left:-4rem;
}

.btn-playlist {
  width: 26%;
  overflow: hidden;
  padding: 1rem;
  display: flex;
  justify-content: center
}

.btn-down {
  transform: rotate(-90deg);
  height:4rem;
  margin-bottom: 0.5rem;
}

.btn-shuffle-play {
  width: 90%;
  height: 4.2rem;
  background-color: #37b349;
  border-radius: 30px;
  margin-bottom: 0.5rem;
  .shuffle-play-text {
    font-size: 20px;
    line-height: 36px;
    color: #ffffff;
    font-family: "Source Sans Pro";
    font-weight: bold;
    text-transform: uppercase;
  }
}
</style>
