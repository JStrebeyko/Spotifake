<template>
<div class="playlist-wrapper">
  <!-- <div class="playlist-head">
    <div class="song-info">
      <div class="name"></div>
      <div class="artist"></div>
    </div>
    <btn play/>
  </div> -->
  <div class="playlist-body">
    <div class="tracklist">
      <div v-for="(track, index) in tracklist" class="track">
        <span>{{index+1}}</span> <span>{{track.title}}</span><span>{{track.duration}}</span>
      </div>
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
  }
}
</script>

<style lang="scss">
.playlist-wrapper {
  width: 576px;
  height: 100%;
  margin-top: 8.1rem;
  position: absolute;
  z-index: 2;
  color: white;
  background-color: rgba(255, 255, 255, 1);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-content: space-around;
  align-items: center;
  text-align: center;
}
/* .playlist-head {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 8.1rem;
  justify-content: space-between;
} */
.playlist-body {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;
  height: 100%;
  /* align-content: space-around; */
  justify-content: space-between;
  margin-bottom: 8.1rem;
}
.tracklist {
  color: black;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  height: 100%;
  &.track {
  text-justify: left;
  }
}
.btn-box {
  display: flex;
  /* align-self:flex-end; */
  flex-direction: column;
  width: 80%;
  align-items: center;

}
</style>
