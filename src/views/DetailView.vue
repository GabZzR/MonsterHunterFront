<template>
  <div>
    <div class="courses-container">
      <div class="course">
        <div class="course-preview">
           <img :src="require(`../assets/img/${movies.name.toLowerCase()}.png`)">
        </div>
        <div class="course-info">
          <h2>{{ movies.name }}</h2>
          <h4>{{ movies.specie }}</h4>
          <h6>{{ movies.nickname }}</h6>
          <h4 v-if="movies.element == null">Element: Physique</h4>
          <h4 v-if="movies.element != null">Element: {{ movies.element }}</h4>
          <h4>weakagainst: {{ movies.weakagainst }}</h4>
          <h4>tailleMin: {{ movies.lengthmin }}</h4>
          <h4>tailleMax: {{ movies.lengthmax }}</h4>
          <h4>generation: {{ movies.generation }}</h4>
          <h4 v-if="movies.agro == true">Aggresif</h4>
          <h4 v-if="movies.agro != true">Passif</h4>
          <span>{{ movies.description }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "DetailView",
  data: () => ({
    movies: {},
  }),
  methods: {},
  async created() {
    let movies = await axios.get(
      "http://localhost:15000/monster/" + this.$route.params.monsterId
    );
    console.log(movies);
    this.movies = movies.data;
    console.log(this.movies);
  },
};
</script>

<style scoped>
img{
  width: 100%;
}
.course-preview{
  width: 25%;
}

</style>