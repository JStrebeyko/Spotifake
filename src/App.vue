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
          cover: require('./assets/cover_2.png'),
          tracks: [
            {
              title: 'Self Conscious',
              duration: '4:21'
            }, {
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
              title: 'Lost in the Worlds',
              duration: '3:11'
            }, {
              title: 'Who Will Survive in America',
              duration:  '3:11'
            }, {
              title: 'Dark Fantasy',
              duration: '3:51'
            }
          ]
        },
        {
          artist: 'Steel Panther',
          title: 'Feel the Steel',
          cover: require('./assets/cover_1.png'),
          tracks: [
            {	title: 'Death to All But Metal',
              duration:	"2:30"
            }, {
              title: 'Asian Hooker',
              duration:	'4:02'
            },{
              title: "Community Property",
              duration:	'3:39'
            },{
              title: "Eyes of a Panther",
              duration:	'3:37'
            },{
              title: "Fat Girl (Thar She Blows)",
              duration:	'4:38'
            },{
              title: "Eatin' Ain't Cheatin'",
              duration:	'3:51'
            },{
              title: "Party All Day (Fuck All Night)",
              duration:	'3:03'
            },{
              title: "Turn Out the Lights",
              duration:	'4:24'
            },{
              title: "Stripper Girl",
              duration:	'3:35'
            },{
              title: "The Shocker",
              duration:	'4:10'
            },{
              title: "Girl from Oklahoma",
              duration:	'3:57'}
          ]
        },
        {
          artist: 'Kanye West',
          title: 'My Beautiful Dark Twisted Fantasy',
          cover: require('./assets/cover_3.png'),
          tracks: [
            {
              title: 'Dark Fantasy',
              duration: '4:40'
            }, {
              title: 'Gorgeous',
              duration: '5:57'
            }, {
              title: 'Power',
              duration: '4:52'
            }, {
              title: 'All of the Lights (Interlude)',
              duration: '1:02'
            }, {
              title: 'All of the Lights',
              duration: '4:59'
            }, {
              title: 'Monster',
              duration: '6:18'
            }, {
              title: 'So Appalled',
              duration: '4:52'
            }, {
              title: 'Devil in a New Dress',
              duration: '6:38'
            }, {
              title: 'Runaway',
              duration: '5:52'
            }, {
              title: 'Hell of a Life',
              duration: '4:52'
            }, {
              title: 'Blame Game',
              duration: '9:08'
            }, {
              title: 'Lost in the World',
              duration: '5:27'
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
  overflow: hidden;
}

/* reset */
*, *:before, *:after {
  box-sizing: border-box;
}
</style>
