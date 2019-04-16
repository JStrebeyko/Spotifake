<template>
<div class="playlist-wrapper">
  <div class="playlist-body">
    <div class="tracklist">
      <div v-for="(track, index) in trimmedTracklist" class="track" :key="index">
        <span class="track-number">{{index+1}}. </span>
        <span class="track-title">{{track.title}}</span>
        <span class="track-duration">{{track.duration}}</span>
      </div>
      <div class="white-gradient"></div>
    </div>
    <div class="btn-box">
      <btn shufflePlay />
      <btn down @click.native="downClicked"/>
    </div>
  </div>
</div>
</template>

<script>
import Btn from './Btn'
export default {
  props: {
    tracklist: {
      type: Array
    }
  },
  components: {
    Btn
  },
  methods: {
    downClicked() {
      this.$emit('closePlaylist')
    }
  },
  computed: {
    trimmedTracklist() {
      return this.tracklist.slice(1,this.tracklist.length)
    }
  }
}
</script>

<style lang="scss">
*{
  box-sizing: border-box
}
.playlist-wrapper {
  width: 576px;
  height: 100%;
  position: absolute;
  display: flex;
  justify-content: space-between;
  align-content: space-around;
  align-items: center;
  // text-align: center;
  margin-top: 8.1rem;
  z-index: 2;
  color: white;
  background-color: rgba(255, 255, 255, 1);
  flex-direction: column;
}

.playlist-body {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;
  height: 100%;
  justify-content: space-between;
  font-family: "Source Sans Pro";
  margin-bottom: 8.1rem;
}
.tracklist {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  color: black;
  position: relative;
  padding-top: 2.1rem;
  .white-gradient {
    width: 100%;
    height: 100%;
    background-image: linear-gradient(rgba(255,255,255,0), rgba(255,255,255,1));
    position: absolute;
    z-index: 1;
  }
  .track {
    width: 100%;
    margin: 1.4rem 0;
    .track-number {
      color: #9a9b9b;
      background:#ffffff;
      padding-left: 4rem;
      padding-right: 1.6rem;
    }
    .track-title {
      font-size: 24px;
      line-height: 20px;
      color: #1b1b1b;
      font-family: "Source Sans Pro";
      background:#ffffff;
      padding-right: 1rem;
      &:after {
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
    }
    .track-duration {
      float: right;
      font-size: 24px;
      line-height: 20px;
      background:#ffffff;
      padding-right: 4rem;
      padding-left: 1rem;
      color: #9a9b9b;
      font-family: "Source Sans Pro";
    }
  }
}

.btn-box {
  display: flex;
  flex-direction: column;
  width: 80%;
  align-items: center;
}

.playlistPlayBtn img {
  position: absolute;
  display: block;
  top: 0;
  right: 33px;
  z-index: 20;
  max-width: 130px;
}
</style>
