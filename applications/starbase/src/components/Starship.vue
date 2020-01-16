<template>
    <p class="card-text">{{starship.name}}</p>
</template>

<script>
  export default {
    props: ['url'],
    data() {
      return {
        starship: {}
      }
    },
    methods: {
      fetchStarship(url) {
        fetch(url, {
          method: 'GET'
        }).then(response => response.json())
          .then(json => this.starship = json);
      }
    }, created() {
      this.fetchStarship(this.url)
    }
  }
</script>
