<template>
<div>
  <div class="all">
  <div class="bg" :style="{ 'background-image': 'url('+bg+')'}">
    <div class="gradient"></div>
  </div>
<div class="wrapper">

  <transition name="moreslide">
    <more v-if="displayMore" @return="toggleMore" :song="currentAlbum.tracks[0].title" :artist="currentAlbum.artist" :artworkPath="currentAlbum.cover"/>
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
    <!-- <slick ref="slick" :options="slickOptions"> -->
      <div class="covers">
        <img v-for="(album, index) in albums"
        :src="album.cover"
        class="album-cover"
        :class="{active: currentAlbumNum===index}"
        >
      </div>
    <!-- </slick> -->

    <div class="now-playing">
      <span class="song">{{currentSong}}</span>
      <span class="artist">{{currentArtist}}</span>
    </div>


    <div class="controls">
      <btn shuffle/>
      <btn prev @click.native="prev"/>
      <btn play :active="isPlaying" @click.native="togglePlay"/>
      <btn next @click.native="next"/>
      <btn repeat/>
    </div>
  </div>

  <div class="feet">
    <btn playlist @click.native="togglePlaylist"/>
    <div class="song-info">
      <span class="next">next</span><br/>
      <div class="next-song-info">
        <span class="song-name">{{currentAlbum.tracks[1].title}}</span>
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
// import Slick from 'vue-slick'
// TODO:
// core:
// [v] menu wysuwane z prawej strony
// [ ] obrazki płyt działają jak slider (slick.js?)
// [v] guzik play zmieniający swój stan
// [v] icona na dole => menu wysuwane z dołu z listą wszystkich utworów

// additional:
// [v] btn
// [] deal with the computed watcher console.error
// [] flow control
// []
export default {
  name: 'player',
  components: {
    More,
    Btn,
    Playlist,
    // Slick
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
      currentAlbum: {},
      slickOptions: {
        arrows: false,
        slidesToShow: 1
      }
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
    },
    next() {
      // this.$refs.slick.next();
      this.changeCurrentAlbum('next')
    },
    prev() {
      // this.$refs.slick.prev();
      this.changeCurrentAlbum()
    },
    changeCurrentAlbum(dir) {
      if (dir==='next') {
        this.currentAlbumNum += 1
        if(this.currentAlbumNum >= this.albums.length) {
          this.currentAlbumNum = 0
        }
      } else {
        this.currentAlbumNum--
        if (this.currentAlbumNum<0) {
          this.currentAlbumNum=this.albums.length-1
        }
      }
        console.log(this.currentAlbumNum)
    }
  },
  computed: {
    playSrc() {
      let picture;
      picture = this.isPlaying ? 'Play_active.png' : 'Play_inactive.png'
      let string = `./../assets/${picture}`
      return string
    },
    currentSong() {
      if (this.currentAlbum) {
        return this.currentAlbum.tracks[0].title
      }
    },
    currentArtist() {
      if (this.currentAlbum) {
        return this.currentAlbum.artist
      }
    }
  },
  watch: {
    currentAlbumNum() {
      this.currentAlbum = this.albums[this.currentAlbumNum]

    }
  }
}
</script>

<style scoped lang="scss">

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
}

.head {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 8.1rem;
  justify-content: space-between;
  z-index: 1;
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
  z-index:1;
  .covers{
    display: flex;
    justify-content: center;
    align-items: center;
    .album-cover {
      width: 12rem;
      height: 12rem;
      margin: 2rem;
      &.active{
        width:20rem;
        height: 20rem;
      }
    }
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
  ". . . . . . . . . . . . . . . . . . . . "
}
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
   transition: 0.6s;
 }
 .moreslide-enter, .moreslide-leave-to {
   transform: translateX(100%);
   opacity:0.25
 }
  .playlistslide-enter-active, .playlistslide-leave-active {
   transition: 0.6s;
 }
 .playlistslide-enter, .playlistslide-leave-to {
   transform: translateY(100%);
   opacity:0.25
 }



</style>

