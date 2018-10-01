<template>
    <button :class="className">
      <img v-if="back" src="./../assets/back_ico.svg"/>
      <img v-if="more" src="./../assets/more_ico.svg"/>
      <img v-if="shuffle && !isToggled" src="./../assets/shuffle_ico.svg"/>
      <svg  v-if="shuffle && isToggled" width="26" height="26" viewBox="0 0 26 26">
        <path id="shuffle_ico" fill="#37b34a" class="cls-1" d="M584.225,790.988a0.322,0.322,0,0,1-.318-0.322v-2.639l-0.4-.02a10.1,10.1,0,0,1-9.032-6.853l-1.89-5.653a7.883,7.883,0,0,0-7.49-5.388H564.06a1.069,1.069,0,1,1,0-2.137h1.03a10.021,10.021,0,0,1,9.5,6.875l1.891,5.653a7.86,7.86,0,0,0,6.978,5.365l0.451,0.029V783.21a0.323,0.323,0,0,1,.323-0.323h0a0.332,0.332,0,0,1,.241.09l4.248,3.534,0.178,0.2a0.336,0.336,0,0,1,.105.244,0.33,0.33,0,0,1-.1.227l-4.459,3.707A0.336,0.336,0,0,1,584.225,790.988Zm0-17.893a0.322,0.322,0,0,1-.32-0.323v-2.689l-0.453.031a7.944,7.944,0,0,0-4.7,1.97,1.07,1.07,0,0,1-.706.266h0a1.092,1.092,0,0,1-.849-0.368,1.066,1.066,0,0,1,.106-1.507,10.2,10.2,0,0,1,6.206-2.5l0.4-.02v-2.639a0.285,0.285,0,0,1,.5-0.224l4.519,3.762a0.324,0.324,0,0,1-.023.444l-4.459,3.708A0.334,0.334,0,0,1,584.227,773.1ZM564.06,788.006a1.068,1.068,0,1,1,0-2.136h1.03a7.937,7.937,0,0,0,4.875-1.68l0.064-.046a1.072,1.072,0,0,1,1.457.161,1.067,1.067,0,0,1-.119,1.506,10.106,10.106,0,0,1-6.277,2.195h-1.03Z" transform="translate(-563 -765)"/>
      </svg>
      <img v-if="prev" src="./../assets/previous_ico.svg"/>
      <img v-if="next" src="./../assets/next_ico.svg"/>
      <img v-if="repeat && !isToggled" src="./../assets/repeat_ico.svg"/>
      <svg v-if="repeat && isToggled" width="26" height="26" viewBox="0 0 26 26">
        <path id="repeat_ico" class="cls-1" fill="#37b34a" d="M1012.06,780.553a1.069,1.069,0,0,1-1.06-1.069V776.5a8.53,8.53,0,0,1,8.52-8.524h12.35v-2.659a0.326,0.326,0,0,1,.32-0.323,0.33,0.33,0,0,1,.19.1l4.5,3.758a0.321,0.321,0,0,1-.02.445L1032.41,773a0.345,0.345,0,0,1-.23.1,0.324,0.324,0,0,1-.31-0.323v-2.659h-12.35a6.4,6.4,0,0,0-6.39,6.387v2.982A1.071,1.071,0,0,1,1012.06,780.553Zm3.75,10.437a0.311,0.311,0,0,1-.2-0.1l-4.51-3.757a0.361,0.361,0,0,1-.07-0.218,0.326,0.326,0,0,1,.1-0.227l4.45-3.707a0.307,0.307,0,0,1,.53.227v2.66h12.36a6.39,6.39,0,0,0,6.38-6.388V776.5a1.07,1.07,0,0,1,2.14,0v2.982a8.53,8.53,0,0,1-8.52,8.524h-12.36v2.66A0.316,0.316,0,0,1,1015.81,790.99Z" transform="translate(-1011 -765)"/>
      </svg>
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
    },
    isToggled: {
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

.btn-shuffle,
.btn-repeat,
.btn-prev,
.btn-next {
  z-index: 3;
}

.btn-play {
  max-width:18rem;
  display: flex;
  margin-left:-4rem;
  margin-right:-4rem;
  img {
    width: 100%
  }
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
  margin-left: 0.4rem;
  margin-bottom: 0.6rem;
}

.btn-shuffle-play {
  width: 96%;
  height: 4.6rem;
  background-color: #37b349;
  border-radius: 30px;
  margin-bottom: 0.6rem;


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
