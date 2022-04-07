<template>
<div>
<div class="new" v-if="displayAdmin == true">Créer un nouveau monstre ➕</div>
  <div class="list">
      
    <table class="styled-table">
      <thead>
        <tr>
          <th>Icone</th>
          <th>Name</th>
          <th>Nickname</th>
          <th>Species</th>
          <th>Element</th>
          <th>Weakness</th>
          <th v-if="displayAdmin == true">Admin</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="monster in movies" :key="monster.id" @click="goToMonster(monster.id)">
          <th><img :src="'../assets/icone/' + monster.name.toLowerCase() + '.png'" alt='affiche' /></th>
          <th>{{monster.name}}</th>
          <th>{{monster.nickname}}</th>
          <th>{{monster.specie}}</th>
          <th><img :src="'../assets/element/' + monster.name.toLowerCase() + '.png'" alt='.' /> {{monster.element}}</th>
          <th><img :src="'../assets/element/' + monster.name.toLowerCase() + '.png'" alt='.' /> {{monster.weakagainst}}</th>
          <th v-if="displayAdmin == true"><span @click.stop="deleteMonster(monsterId)">🚮</span> | <span>🖋</span></th>
        </tr>
      </tbody>
    </table>
  </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "MonsterList",
  data: () => ({
    movies:{},

  }),
  props:{
      displayAdmin:{
          type: Boolean,
          required:true
      }
  },
  methods: {
    goToMonster(monsterId){
        this.$router.push({name: 'detail' , params: {monsterId}})
    },
    async deleteMonster(monsterId){

       const del = await axios.delete("http://localhost:15000/monster/delete",{id:monsterId})
       console.log(del);
    }
  },
  async created() {
    let movies = await axios.get("http://localhost:15000/monsters");
    console.log(movies);
    this.movies = movies.data;
    console.log(this.movies);
  },
};
</script>

<style scoped>
tbody tr{
  cursor: pointer;
}
.list {
  display: flex;
  justify-content: center;
}
.styled-table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 0.9em;
  font-family: sans-serif;
  min-width: 800px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}
.styled-table thead tr {
  background-color: #009879;
  color: #ffffff;
}
.styled-table th,
.styled-table td {
  padding: 12px 15px;
}
.styled-table tbody tr {
  border-bottom: 1px solid #dddddd;
}

.styled-table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}

.styled-table tbody tr:last-of-type {
  border-bottom: 2px solid #009879;
}

.styled-table tbody tr.active-row {
  font-weight: bold;
  color: #009879;
}
</style>