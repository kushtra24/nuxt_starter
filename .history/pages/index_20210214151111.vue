<template>
<div class="container">
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active"><nuxt-link to="/" class="nav-link">Kërko emër</nuxt-link></li>
          <li class="nav-item"><nuxt-link to="/articles" class="nav-link">Keshilla</nuxt-link></li>
          <li class="nav-item"><nuxt-link to="/about" class="nav-link">Rreth nesh</nuxt-link></li>
          <li class="nav-item"><nuxt-link to="/login" class="nav-link">Kyqu</nuxt-link></li>
        </ul>
      </div>
    </nav>

    <div class="row">
      <div class="col-md-4 search-baby-name">
        <a class="navbar-brand col-md-4" href="#"><Logo /></a>
        <form @submit.prevent="nonVuexSubmit">
          <div class="form-group">
            <div class="form-group">
              <select class="form-control" v-model="ngjyra">
                <option disabled value="">zgjedh nje</option>
                <option>e bardh</option>
                <option>e zez</option>
                <option>e kuqe</option>
                <option>e kaltert</option>
                <option>e omel</option>
              </select>
            </div>

            <div class="here"> {{ ngjyra }}</div>

            <div class="form-group">
              <select class="form-control">
                <option disabled value="">zgjedhe</option>
                <option>10</option>
                <option>20</option>
                <option>Anglisht</option>
                <option>Franceze</option>
                <option>italiane</option>
              </select>
            </div>

            <button type="submit" class="btn btn-primary mt-3">Submit</button>
          </div>
        </form>
      </div>
      <div class="col-8">
          <p v-for="hamam in jokes" :key="hamam.id">
            {{ hamam.joke }}
          </p>
      </div>
    </div>
<!-- <p class="get-me-the-stuff" @click="getMeTheStuff">get me the stuff baby</p> -->
  </div>
</div>
</template>

<script>

export default {

  data() {
    return {
      jokes: [],
      ngjyra: ''
    }
  },

  methods: {

    async nonVuexSubmit() {

      const config = {
        headers: {
          'Accept': 'application/json'
        }
      };

        const url = `https://icanhazdadjoke.com/search`;

        await this.$axios.get(url, config)
        .then((response) => {
          this.jokes = response.data.results;
          console.log('jokes --> ', this.jokes);
        })
        .catch( (error) => {
          console.log('nope', error);
        });
    },

  }

}

</script>