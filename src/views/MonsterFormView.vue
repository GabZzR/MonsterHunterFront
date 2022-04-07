<template>
  <div class="form">
    <form action="localhost:15000/monster" method="post">
        <div>
            <label for="name">Nom: </label>
            <input type="text" name="name" id="name">
        </div>
        <div>
            <label for="nickname">Nickname: </label>
            <input type="text" name="nickname" id="nickname">
        </div>
        <div>
            <textarea name="description" id="description">f</textarea>
        </div>
        <div> <input type="text" name="nickname" id="nickname"></div>
        <div>
        <label for="specie">Espèce: </label>
        
        <input type="text" name="specie" id="specie"></div>
        <div>
            <label for="element">Element: </label>
            
            <input type="text" name="element" id="element">
        </div>
        <div>
            <label for="weakagainst">Faible contre: </label>
            
            <input type="text" name="weakagainst" id="weakagainst">
        </div>

          <div>
            <label for="lenghtmin">Taille min: </label>
            
            <input type="text" name="lenghtmin" id="lenghtmin">
        </div>
        <div>
            <label for="lenghtmmax">Taille max: </label>
            
            <input type="text" name="lenghtmax" id="lenghtmax">
        </div>
        <div>
            <label for="generationx">Generation: </label>
            
            <input type="text" name="generation" id="generation">
        </div>
        <div>
            <label for="agro">Agressif: </label>
            
            <input type="radio" name="agro" id="agro">
        
        </div>
    


            <button type="submit" @click="insertMonster()">Valider</button>
    </form>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: "MonsterFormView",
  data: () => ({
          form:{
              name:"test"
          }
  }),
  methods: {
     async insertMonster(){
          await axios.post("http://localhost:15000/monster",this.form)
      }
  },
  components:{

  }
};

</script>

<style scoped>

</style>