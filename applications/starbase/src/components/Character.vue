<template>
  <div class="col-md-4" @click="switchCharacter">
    <div class="character-card">
      <div class="card-block">
        <h3 class="card-title">{{character.name}}</h3>
        <p class="card-text"> Height: {{character.height}}cm</p>
        <p class="card-text"> Mass: {{character.mass}}kg</p>
        <p class="card-text"> Hair Color: {{character.hair_color}}</p>
        <p class="card-text"> Eye Color: {{character.eye_color}}</p>
        <div v-if="character.homeworld">
          <Planet v-bind:url="character.homeworld"/>
        </div>
        <div v-if="character.starships != ''">
          <p class="card-text">Starships: </p>
          <div v-for="starship in character.starships">
            <Starship v-bind:url="starship"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Planet from "./Planet";
  import Starship from "./Starship";

  export default {
    props: [
      'id'
    ],
    data() {
      return {
        character: {}
      }
    },
    methods: {
      fetchCharacter(id) {
        fetch(`https://swapi.co/api/people/${id}`, {
          method: 'GET'
        }).then(response => response.json())
          .then(json => this.character = json);
      },
      switchCharacter() {
        let random_id = Math.floor(Math.random() * 83) + 1;
        this.fetchCharacter(random_id)
      }
    },
    created() {
      this.fetchCharacter(this.id);
    },
    components: {
      Planet,
      Starship,
    }
  }
</script>
