<template>
  <div>
    <p class="card-text">Homeworld: {{planet.name}}</p>
  </div>
</template>
<script>
  export default {
    props:
      ['url'],
    data() {
      return {
        planet: {}
      }
    },
    methods: {
      fetchPlanet(url) {
        fetch(url, {
          method: 'GET'
        }).then(response => response.json())
          .then(json => this.planet = json);
      }
    },
    created() {
      this.fetchPlanet(this.url)
    },
  }
</script>
