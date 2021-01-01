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
        <div class="card-title">Name</div>
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
  background-color: #97ce4c;
}
.indexes {
  border-radius: 50%;
  width: 50px;
  line-height: 50px;
  background: #44281d;
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
  top: 50%;
  transform: translate(-50%, -50%);
}

.cards {
  position: relative;
  border: #dedede solid 1px;
  height: 210px;
  width: 160px;
  background-color: #e4a788;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
  transition: 0.5s;
}
.cards:not(:first-child) {
  margin-left: -20px;
}
.cards:hover {
  transform: translateY(-100px);
  transition: 0.5s;
}
.cards:hover {
  ~ .cards {
    transform: translateX(80px);
  }
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
