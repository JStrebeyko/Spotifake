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
      <p v-if="shufflePlay" class="shuffle-play-text">shuffle play</p>
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
    }
  },
  mounted() {

  },
  computed: {
    className() {
      let className;
      this.back && (className = 'btn-back');
      this.more && (className = 'btn-more');
      this.shuffle && (className = 'btn-shuffle');
      this.prev && (className = 'btn-prev');
      this.play && (className = 'btn-play');
      this.next && (className = 'btn-next');
      this.repeat && (className = 'btn-repeat');
      this.playlist && (className = 'btn-playlist');
      this.down && (className = 'btn-down');
      this.shufflePlay && (className = 'btn-shuffle-play');
      return className;
    }
    // src() {
    //   return this.back ? './../assets/back_ico.svg': false
    // }
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
.btn-more img {
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
}

.btn-shuffle-play {
  width: 80%;
  text-transform: uppercase;
  background-color: #37b349;
  border-radius: 30px;
}
</style>
