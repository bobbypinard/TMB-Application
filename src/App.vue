<template>
  <div id="app">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

      <h1 class="header">Swifting through the years</h1>

      <div class="container">
      <h2 class="title tile">Country Taylor: <em>Circa. 2003-2010</em></h2>
      <div class="tile">
        <iframe class="vid" frameborder="0" :src="country.id"></iframe>
        <h3> {{ country.title }}</h3><br />
      </div>

      <h2 class="title tile">Pop Taylor: <em>2011-2016</em></h2>
      <div class="tile">
        <iframe class="vid" frameborder="0" :src="pop.id"></iframe>
        <h3> {{ pop.title }}</h3><br />
      </div>

      <h2 class="title tile">Technopop Taylor: <em>2017-Present</em></h2>
      <div class="tile">
        <iframe class="vid" frameborder="0" :src="technoPop.id"></iframe>
        <h3> {{ technoPop.title }}</h3><br />
      </div>

      <div class="sad">
        <h2 class="title tile">Come back Taylor, we miss you.</h2>
        <iframe class="vid" :src="crying.id" frameborder="0"></iframe>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
  data () {
    return {
      country: {
        title: "",
        id: "",
        errors: []
      },

      pop: {
        title: "",
        id: "",
        errors: []
      },

      technoPop: {
        title: "",
        id: "",
        errors: []
      },
      crying: {
        title: "",
        id: "https://youtube.com/embed/Uf9nS145e18",
        errors: []
      }
    }
  },
  created() {
    axios.get(`https://www.googleapis.com/youtube/v3/search?key=%20AIzaSyC4pukMV-gg9zWYLi4wwcTWPmqeixNTbU4&id=xKCek6_dB0M&part=snippet&q=Taylor%20Swift%20-%20Teardrops%20On%20My%20Guitar&order=relevance`)
    .then(response => {
      this.country.title = response.data.items[0].snippet.title
      this.country.id = "https://youtube.com/embed/" + response.data.items[0].id.videoId

    })
    .catch(e => {
      this.coutry.errors.push(e)
    })

    axios.get('https://www.googleapis.com/youtube/v3/search?key=%20AIzaSyC4pukMV-gg9zWYLi4wwcTWPmqeixNTbU4&id=xKCek6_dB0M&part=snippet&q=Taylor%20Swift%20-%20Shake%20It%20Off&order=relevance')
    .then(response => {
      this.pop.title = response.data.items[0].snippet.title
      this.pop.id = "https://youtube.com/embed/" + response.data.items[0].id.videoId
    })
    .catch(e => {
      this.pop.errors.push(e)
    })

    axios.get('https://www.googleapis.com/youtube/v3/search?key=%20AIzaSyC4pukMV-gg9zWYLi4wwcTWPmqeixNTbU4&id=xKCek6_dB0M&part=snippet&q=Taylor%20Swift%20-%20...Ready%20For%20It?&order=relevance')
    .then(response => {
      this.technoPop.title = response.data.items[0].snippet.title
      this.technoPop.id = "https://youtube.com/embed/" + response.data.items[0].id.videoId
    })
    .catch(e => {
      this.technoPop.errors.push(e)
    })
  }

}
</script>

<style>
#app {
  background-image: url("./assets/Taylor.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
  margin: -22px -8px;
  color: #F0F0F0;
  font-family: Helvetica, sans-serif;
  height: 50%;
}

.container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 3em;
  align-items: center;
  justify-items: center;
}

.header {
  text-align: center;
}

.vid {
  height: 20em;
  width: 35em;
}

.tile {
  justify-self: stretch;
  text-align: center;
}

.title {
  font-size: 2em;
  align-self: center;
}

.sad {
  grid-column: span 2;
  justify-self: center;
  text-align: center;
}

@media screen and (max-width: 650px) {
  .vid {
    height: 14em;
    width: 25em;
  }
}

@media screen and (max-width: 1150px) {
  .container {
    grid-template-columns: 1fr;
  }
  .sad {grid-column: 1;}
}

@media screen and (min-width: 1921px) {
  #app {
    background-image: none;
    background-color: #FFF;
    color: darkred;
  }
}
</style>
