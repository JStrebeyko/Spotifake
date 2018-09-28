<template>
<div>
  <div class="all">
  <div class="bg" :style="{ 'background-image': 'url('+bg+')'}">
    <div class="gradient"></div>
  </div>
<div class="wrapper">

  <transition name="moreslide">
    <more v-if="displayMore" @return="toggleMore"/>
  </transition>
  <div class="head">
    <btn back/>
      <div class="album-info">
        <span class="album">album</span>
        <span class="album-name">{{currentAlbum.title}}</span>
      </div>
    <btn more @click.native="toggleMore"/>
  </div>

  <div class="body">
    <div class="controls">
      <btn shuffle/>
      <btn prev/>
      <btn play :active="isPlaying" @click.native="togglePlay"/>
      <btn next/>
      <btn repeat/>
    </div>
  </div>

  <div class="feet">
    <btn playlist @click.native="togglePlaylist"/>
    <div class="song-info">
      <span class="next">next</span><br/>
      <div class="next-song-info">
        <span class="song-name">Livin' in A Movie</span>
        <span class="next-time">3:27</span>

      </div>
    </div>
  </div>
  <transition name="playlistslide">
    <playlist v-if="displayPlaylist" @closePlaylist="togglePlaylist" :tracklist="currentAlbum.tracks"/>
  </transition>
</div>
</div>
</div>
</template>

<script>
import More from './../components/More'
import Playlist from './../components/Playlist'
import Btn from './../components/Btn'
import bg from '@/assets/bg_photo.png'
// TODO:
// core:
// [v] menu wysuwane z prawej strony
// [] obrazki płyt działają jak slider (slick.js?)
// [v] guzik play zmieniający swój stan
// [v] icona na dole => menu wysuwane z dołu z listą wszystkich utworów

// additional:
// [v] btn
// []
// []
export default {
  name: 'player',
  components: {
    More,
    Btn,
    Playlist
  },
  props: {
    albums: {
      type: Array
    }
  },
  data() {
    return {
      isPlaying: false,
      displayMore: false,
      displayPlaylist: false,
      bg,
      currentAlbumNum:0,
      currentAlbum: {}
    }
  },
  mounted() {
    this.currentAlbum = this.albums[this.currentAlbumNum];
  },
  methods: {
    togglePlay() {
      console.log(this.isPlaying)
      this.isPlaying = !this.isPlaying
    },
    toggleMore() {
      this.displayMore = !this.displayMore;
    },
    togglePlaylist() {
      this.displayPlaylist = !this.displayPlaylist
    }
  },
  computed: {
    playSrc() {
      let picture;
      picture = this.isPlaying ? 'Play_active.png' : 'Play_inactive.png'
      let string = `./../assets/${picture}`
      return string
    }
  }
}
</script>

<style scoped lang="scss">
/* unstyle buttons: */

.all {
  width: 576px;
  height: 1024px;
  position: relative;
}

  .bg {
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  filter: grayscale(100%);
  position: absolute;
  right: 0;
  left: 0;
  height: 50%;
  width: 100%;
  display: block;
  z-index:1;
  }
  div.gradient {
    background: rgba(27, 27, 27, 0.95);
    z-index:3;
    display: block;
    position: absolute;
    width: 100%;
    height: 100%;
  }
.wrapper {
  background-color: #1b1b1b;
  width: 100%;
  height: 100%;
  display: flex;
  position:relative;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;
  // background-image: url("./../assets/bg-photo.png")
}
.head {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 8.1rem;
  justify-content: space-between;
  z-index: 1;
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
.album-info{
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.album {
  font-size: 18px;
  line-height: 33px;
  color: #9a9b9b;
  font-family: "Source Sans Pro";
  text-transform: uppercase;
  text-align: center;
}
.album-name {
  font-size: 24px;
  line-height: 25px;
  color: #ffffff;
  font-family: "Source Sans Pro";
  text-align: center;

}

.body {
  .controls {
    display: flex;
    justify-content: space-around;
    padding: 0 1rem;

  }
}
.feet {
  width: 576px;
  height: 89px;
  background-color: #ffffff;
  display: flex;
}
span.next {
  font-size: 18px;
  line-height: 36px;
  color: #9a9b9b;
  font-family: "Source Sans Pro";
  text-align: left;
  text-transform: uppercase;
}

.song-info {
  padding: 0.75rem;
  overflow-x: hidden;
  width: 100%;
}
.song-name {
  font-size: 24px;
  line-height: 20px;
  color: #1b1b1b;
  font-family: "Source Sans Pro";
  background:#ffffff;
  padding-right: 1rem;
}
.song-name:after {
    float: left;
    width: 0;
    font-size: 1.5rem;
    color: #9a9b9b;
    white-space: nowrap;
    letter-spacing: 2px;
    content:
 ". . . . . . . . . . . . . . . . . . . . "
 ". . . . . . . . . . . . . . . . . . . . "
 ". . . . . . . . . . . . . . . . . . . . "
 ". . . . . . . . . . . . . . . . . . . . "}
 .next-time {
   float: right;
   font-size: 24px;
   line-height: 20px;
    background:#ffffff;
    padding-right: 2rem;
    padding-left: 1rem;
    color: #9a9b9b;
    font-family: "Source Sans Pro";
 }

 .next-song-info {
   overflow: hidden;
 }
 .moreslide-enter-active, .moreslide-leave-active {
   transition: 1s;
 }
 .moreslide-enter, .moreslide-leave-to {
   transform: translateX(100%);
   opacity:0
 }
  .playlistslide-enter-active, .playlistslide-leave-active {
   transition: 1s;
 }
 .playlistslide-enter, .playlistslide-leave-to {
   transform: translateY(100%);
   opacity:0
 }

</style>

