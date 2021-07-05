<template>
  <div id="app">
    <Header/>
    
    <div class="container">
      <table class="apiTable">
        <tr>
          <th>Name</th>
          <th>Programming Language</th>
          <th>Star Count <button v-on:click="sortStarsAsc()">Asc</button><button v-on:click="sortStarsDesc()">Desc</button></th>
          <th>Fork Count <button v-on:click="sortForksAsc()">Asc</button><button v-on:click="sortStarsDesc()">Desc</button></th>
          <th>Authors Avatar</th>
        </tr>
        <tr v-for="apis in popularAPIs" v-bind:key="apis.name">
          <td>{{apis.name}}</td>
          <td>{{apis.language}}</td>
          <td>{{apis.stars}}</td>
          <td>{{apis.forks}}</td>
          <td><img class="author-avatar" :src="apis.avatar"></td>
        </tr>
      </table>
    </div>
    <ul v-for="lang in popularLangs.slice(0,10)" v-bind:key="lang">
      <li>{{lang}}</li>
    </ul>
  </div>
</template>

<script>
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    Header,
  },
  data: function(){
    return {
      popularLangs: [],
      popularAPIs: [],
      sortStarAsc: false,
      sortForkAsc: false
    }
  },
  created: function() {
    this.getPopularAPIs(),
    this.getPopularLangs()
  },
  methods: {
    getPopularAPIs(){
      fetch('https://api.trending-github.com/github/repositories')
      .then(response => response.json())
      .then(
        data => (this.popularAPIs = data));
    },

     getPopularLangs(){
       
      
      fetch('https://api.trending-github.com/github/languages')
      .then(response => response.json())
      .then(data => (this.popularLangs = data));

    },

    
    sortForksAsc(){
      this.popularAPIs.sort(this.compareForksAsc);
      },
    sortStarsAsc(){
      this.popularAPIs.sort(this.compareStarsAsc);
      },
    sortForksDesc(){
      this.popularAPIs.sort(this.compareForksDesc);
      },
    sortStarsDesc(){
      this.popularAPIs.sort(this.compareStarsDesc);
      },
    compareForksAsc(a, b) {
      const forkA = a.forks;
      const forkB = b.forks;

      let comparison = 0;
      if (forkA > forkB) {
        comparison = 1;
      } else if (forkA < forkB) {
        comparison = -1;
      }
        return comparison;
      },

    compareStarsAsc(a, b) {
      const starA = a.stars;
      const starB = b.stars;

      let comparison = 0;
      if (starA > starB) {
        comparison = 1;
      } else if (starA < starB) {
        comparison = -1;
      }
        return comparison;
      },

       compareForksDesc(a, b) {
      const forkA = a.forks;
      const forkB = b.forks;

      let comparison = 0;
      if (forkA > forkB) {
        comparison = 1;
      } else if (forkA < forkB) {
        comparison = -1;
      }
        return comparison * -1;
      },

    compareStarsDesc(a, b) {
      const starA = a.stars;
      const starB = b.stars;

      let comparison = 0;
      if (starA > starB) {
        comparison = 1;
      } else if (starA < starB) {
        comparison = -1;
      }
        return comparison * -1;
      }


    }
  }
  
  
    
    
  

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  display: flex;
  justify-content: center;
}

.author-avatar {
  width: 100px;
  height: 100px;
}

li {
  list-style: none;
}

</style>
