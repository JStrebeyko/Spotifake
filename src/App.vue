<template>
  <div id="app">
    <player :albums="albums"/>
  </div>
</template>

<script>
import Player from './views/Player'

export default {
  name: 'app',
  components: {
    Player
  },
  data() {
    return {
      albums: [
        {
          artist: 'Kanye West',
          title: 'Unreleased',
          tracks: [
            {
              title: 'Livin\' In A Movie',
              duration: '3:27'
            }, {
              title: 'Dark Fantasy',
              duration: '5:12'
            }, {
              title: 'All of the Lights',
              duration:  '2:54'
            }, {
              title: 'So Appalled',
              duration: '3:51'
            }, {
              title: 'Devil in a New Dress',
              duration: '4:51'
            }, {
              title: 'Runaway',
              duration: '3:46'
            }, {
              title: 'Hell of a Life',
              duration: '3:09'
            }, {
              title: 'Blame Game',
              duration: '7:02'
            }, {
              title: 'Lost in the Worls',
              duration: '3:11'
            }, {
              title: 'Who Will Survive in America',
              duration:  '3:11'
            }, {
              title: 'Dark Fantasy',
              duration: '3:51'
            }
          ]
        }
      ]
    }
  }
}
</script>

<style>
body {
  margin: 0
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #37b349;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}
</style>
