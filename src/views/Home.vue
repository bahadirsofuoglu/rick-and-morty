<template>
  <div>
    <div class="card-title">Episodes</div>
    <hr />
    <a
      class="indexes"
      v-for="index in 20"
      :key="index"
      @click="fetchEpisodes(index)"
      >{{ index }}</a
    >

    <div class="container">
      <div
        class="cards"
        v-for="(character, index) in characters"
        :key="character.id"
        @click="showCard(index)"
      >
        <img class="card-img-cplus" :src="character.image" />

        <div class="card-title">Name</div>
        <div class="card-des">
          {{ character.name }}
        </div>
      </div>
    </div>

    <div class="selectedCard" v-if="showId !== null">
      <img class="selected-card-img-cplus" :src="characters[showId].image" />

      <div class="selected-card-title">Name</div>
      <div class="selected-card-des">
        {{ characters[showId].name }}
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
      characters: [],
      showId: null
    }
  },
  mounted () {
    this.fetchEpisodes()
  },
  methods: {
    async fetchEpisodes (index) {
      this.characters = []
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
    },
    showCard (id) {
      this.showId = id
      console.log(this.showId)
    }
  }
}
</script>
<style lng="scss">
body {
  background-color: #95a58b;
}
.indexes {
  border-radius: 50%;
  width: 50px;
  line-height: 50px;
  background: #4f484a;
  color: white;
  border: 1.5px solid #fbcfce;
  position: absolue;
  text-align: center;
  float: left;
  margin-left: 4px;
}
.container {
  display: flex;
  position: absolute;
  left: 50%;
  top: 30%;
  transform: translate(-50%, -50%);
}
.selectedCard {
  position: absolute;
  left: 40%;
  top: 50%;
  border: #eabde0 solid 1px;
  height: 300px;
  width: 300px;
  background-color: #eabde0;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
}
.selected-card-img-cplus {
  background-repeat: no-repeat;
  background-size: contain;
  margin-top: 30px;
  height: 150px;
  width: 150px;
  border-radius: 50%;
  margin-right: auto;
  margin-left: 75px;
  border: none;
}
.selected-card-title {
  padding-top: 20px;
  padding-left: 10px;
  font-size: 17px;
  font-weight: 600;
  margin-left: 75px;
  font-family: 'Merriweather Sans', sans-serif;
}
.selected-card-des {
  padding-top: 10px;
  padding-left: 10px;
  font-size: 20px;
  font-weight: 100;
  max-width: 140px;
  margin-left: 75px;
  color: #767676;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  max-height: 70px;
  font-family: 'Merriweather Sans', sans-serif;
}
.cards {
  position: relative;
  border: #eabde0 solid 1px;
  height: 210px;
  width: 160px;
  background-color: #eabde0;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
  transition: 0.2s;
}
.cards:not(:first-child) {
  margin-left: -40px;
}
.cards:hover {
  transform: translateY(-50px);
  transition: 0.5s;
}
.cards:hover {
  transform: translateX(-40px);
}

.card-img-cplus {
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
  font-size: 15px;
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
