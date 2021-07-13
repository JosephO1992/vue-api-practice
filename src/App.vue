<template>
  <div id="app">
    <Header/>
    <Table v-bind:popularAPIs="popularAPIs"/>
    <List v-bind:popularLangs="popularLangs"/>

  </div>

  
</template>



<script>
import Header from './components/Header.vue';
import Table from './components/Table.vue';
import List from './components/List.vue';

export default {
  name: 'App',
  components: {
    Header,
    Table,
    List
  },
  data: function(){
    return {
      popularLangs: [],
      popularAPIs: [],
      showDetails: false,
      
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
  flex-direction: column;
  margin: auto
}

.author-avatar {
  width: 100px;
  height: 100px;
}

li {
  list-style: none;
}

@media (max-width: 550px) {
  .responsive {
    display: none;
  }
}

</style>
