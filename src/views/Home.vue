<template>
  <div>
    <a
      class="indexes"
      v-for="index in 20"
      :key="index"
      @click="fetchEpisodes(index)"
      >{{ index }}</a
    >
    <div class="container">
      <div class="cards" v-for="character in characters" :key="character.id">
        <div class="card-img-cplus">
          <img class="card-img-cplus" :src="character.image" />
        </div>
        <div class="card-title">Episode-{{ character.id }}</div>
        <div class="card-des">
          {{ character.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Home',
  data () {
    return {
      episodes: [],
      characters: []
    }
  },
  mounted () {
    this.fetchEpisodes()
  },
  methods: {
    async fetchEpisodes (index) {
      console.log(index)
      let response = await axios.get(
        `https://rickandmortyapi.com/api/episode/${index}`
      )
      response.data.characters.forEach(async element => {
        let res = await axios.get(element)

        this.characters.push({
          name: res.data.name,
          image: res.data.image
        })
        console.log(this.characters)
      })
    }
  }
}
</script>
<style lng="scss">
body {
  background-color: #ecfcff;
}
.indexes {
  height: 3px;
  width: 3px;
  border-radius: 3px;
  margin-left: 3px;
  background: black;
  color: white;
}
.container {
  display: flex;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.cards {
  position: relative;
  border: #dedede solid 1px;
  height: 210px;
  width: 160px;
  background-color: white;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
  transition: 0.5s;
}
.cards:not(:first-child) {
  margin-left: -80px;
}
.cards:hover {
  transform: translateY(-20px);
  transition: 0.5s;
}
.cards:hover {
  ~ .cards {
    transform: translateX(80px);
  }
}
.card-img-python {
  background-color: #a72693;
  background-image: url('https://cdn.auth0.com/blog/python-restful/logo.png');
  background-repeat: no-repeat;
  background-size: contain;
  margin-top: 15px;
  height: 70px;
  width: 70px;
  border-radius: 50%;
  margin-right: auto;
  margin-left: auto;
  border: none;
}
.card-img-cplus {
  /*   background-image: url('data:image/png;base64,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'); */
  background-repeat: no-repeat;
  background-size: contain;
  margin-top: 15px;
  height: 70px;
  width: 70px;
  border-radius: 50%;
  margin-right: auto;
  margin-left: auto;
  border: none;
}
.card-img-code {
  background-color: #a72693;
  background-image: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRhhUT-q0vJ4PZOyUSVG0ZFl9qxcP3VNzLMrQYq9KXPQyqrbGcxlg');
  background-repeat: no-repeat;
  background-size: contain;
  margin-top: 15px;
  height: 70px;
  width: 70px;
  border-radius: 50%;
  margin-right: auto;
  margin-left: auto;
  border: none;
}
.card-title {
  padding-top: 20px;
  padding-left: 10px;
  font-size: 17px;
  font-weight: 600;
  font-family: 'Merriweather Sans', sans-serif;
}
.card-des {
  padding-top: 10px;
  padding-left: 10px;
  font-size: 10px;
  font-weight: 100;
  max-width: 140px;
  color: #767676;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  max-height: 70px;
  font-family: 'Merriweather Sans', sans-serif;
}
</style>
