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
        <div class="album-info" v-if="!displayPlaylist">
          <span class="album">album</span>
          <span class="album-name">{{currentAlbum.title}}</span>
        </div>
        <div class="playlist-head" v-if="displayPlaylist">
          <span class="song">{{currentSong}}</span>
          <span class="artist">{{currentAlbum.artist}}</span>
          <btn play class="playlistPlayBtn" :active="isPlaying" @click.native="togglePlay"/>
        </div>
      <btn more @click.native="toggleMore" v-if="!displayPlaylist"/>
    </div>

    <div class="body">
      <div class="covers">
        <div class="album-cover">
            <img
              :src="prevAlbum.cover"
              :key="prevAlbum.title"
              @click="currentAlbumNum=changeCurrentAlbumNumber()"/>
        </div>
        <div class="album-cover">
            <img
            :src="currentAlbum.cover"
            class="active album-cover"
            :key="currentAlbum.title"/>
        </div>

        <div class="album-cover">
          <img
          :src="nextAlbum.cover"
          :key="nextAlbum.title"
          @click="currentAlbumNum=changeCurrentAlbumNumber('next')"/>
        </div>

      </div>

      <div class="now-playing">
        <span class="song">{{currentSong}}</span>
        <span class="artist">{{currentArtist}}</span>
      </div>

      <div class="controls">
        <btn shuffle :isToggled="isShuffleOn" @click.native="isShuffleOn=!isShuffleOn"/>
        <btn prev @click.native="prev"/>
        <btn play :active="isPlaying" @click.native="togglePlay"/>
        <btn next @click.native="next"/>
        <btn repeat :isToggled="isRepeatOn" @click.native="isRepeatOn=!isRepeatOn"/>
      </div>
    </div>

    <img class="running-track" :src="track"/>
    <div class="feet">
      <btn playlist @click.native="togglePlaylist"/>
      <div class="song-info">
        <span class="next">next</span><br/>
        <div class="next-song-info">
          <span class="song-name">{{this.albums[this.currentAlbumNum].tracks[1].title}}</span>
          <span class="next-time">{{this.albums[this.currentAlbumNum].tracks[1].duration}}</span>
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
import track from '@/assets/running_track.jpg'
// import Slick from 'vue-slick'
// TODO:
// core:
// [v] right 'more' menu
// [v] album covers slider
// [v] play button with state
// [v] playlist menu
// [v] responsiveness

// additional:
// [v] btn
// [v] deal with the computed watcher console.error
// [v] flow control
// toggleable buttons
// dataset from outside
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
      track,
      currentAlbumNum:0,
      currentAlbum: {},
      prevAlbum:{},
      nextAlbum: {},
      isShuffleOn: false,
      isRepeatOn: false
    }
  },
  mounted() {
    this.currentAlbum = this.albums[this.currentAlbumNum];
    this.nextAlbum = this.albums[this.changeCurrentAlbumNumber('next')]
    this.prevAlbum = this.albums[this.changeCurrentAlbumNumber()]
  },
  methods: {
    togglePlay() {
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
      this.currentAlbumNum = this.changeCurrentAlbumNumber('next')
    },
    prev() {
      // this.$refs.slick.prev();
      this.currentAlbumNum = this.changeCurrentAlbumNumber()
    },
    changeCurrentAlbumNumber(dir) {
      let number = this.currentAlbumNum
      if (dir==='next') {
        number += 1
        if(number >= this.albums.length) {
          number = 0
        }
      } else {
        number--
        if (number<0) {
          number=this.albums.length-1
        }
      }
      return number
    }
  },
  computed: {
    currentSong() {
        return this.currentAlbum.tracks ? this.currentAlbum.tracks[0].title : false
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
      this.nextAlbum = this.albums[this.changeCurrentAlbumNumber('next')]
      this.prevAlbum = this.albums[this.changeCurrentAlbumNumber()]
    }
  }
}
</script>

<style scoped lang="scss">

.all {
  max-width: 576px;
  height: 1024px;
  position: relative;
  box-shadow: 10px 10px 200px 10px #000;
  margin: auto;
  position: absolute;
  top: 0; left: 0; bottom: 0; right: 0;
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
  max-width: 100%;
  display: block;
  z-index:1;
}

div.gradient {
  background: linear-gradient(rgba(27, 27, 27, 0.85), rgba(27, 27, 27, 1));
  z-index:3;
  display: block;
  position: absolute;
  width: 100%;
  height: 100%;
}

.wrapper {
  background-color: #1b1b1b;
  max-width: 100%;
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
  max-width: 100%;
  height: 8.1rem;
  justify-content: space-between;
  z-index: 1;
  .playlist-head {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 1rem 3.5rem;
    .song {
      color: #37b34a;
      font-family: "Source Sans Pro";
      font-size: 24px;
      line-height: 25px;
    }
    .artist {
      color: #9a9b9b;
      font-family: "Source Sans Pro";
      font-size: 18px;
      line-height: 25px;
    }
  }
}

.album-info{
  display: flex;
  justify-content: center;
  flex-direction: column;
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
      img {
        width: 8rem;
        height: 8rem;
        margin: 2rem;
      }
      &.active {
        width: 50vw;
        max-width: 20rem;
        height: 50vw;
        max-height: 20rem;
      }
    }
  }
  .now-playing {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 234px;
    .song {
      font-size: 36px;
      line-height: 36px;
      color: #37b34a;
      font-family: "Source Sans Pro";
      text-align: center;
      cursor: pointer;
      &:hover {
        text-shadow: 1px 1px 2px #37b34a,
                    -1px -1px 2px #37b34a
      }
    }
    .artist {
      font-size: 18px;
      line-height: 36px;
      color: #9a9b9b;
      font-family: "Source Sans Pro";
      text-align: center;
      text-transform: uppercase;
      cursor: pointer;
      z-index: 3;
      &:hover {
        text-shadow: 1px 1px 1px #9a9b9b,
                    -1px -1px 1px #9a9b9b
      }
    }
  }
  .controls {
    display: flex;
    justify-content: space-around;
    padding: 0 1rem;
    position: absolute;
    width: 100%;
    bottom: 189px;
    padding: 0 1.5rem;
  }
}
.running-track {
  bottom: 86px;
  position: absolute;

}
.feet {
  max-width: 576px;
  height: 88px;
  background-color: #ffffff;
  display: flex;
  margin-bottom: -1px;
  margin-top: 116px;
  overflow: hidden;
  span.next {
    font-size: 18px;
    line-height: 35px;
    color: #9a9b9b;
    font-family: "Source Sans Pro";
    text-align: left;
    text-transform: uppercase;
  }
  .song-info {
    padding-top: 0.75rem;
    padding-right: 2rem;
    overflow: hidden;
    width: 100%;
    line-height: 20px;
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
      max-width: 0;
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
  }
  .next-song-info {
    overflow: hidden;
  }
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

