<template>
  <div id="app">
    <Header/>
    <div class="container direction">
      <h2>Top 10 Most Popular languages</h2>
    <ul v-for="lang in popularLangs.slice(0,10)" v-bind:key="lang">
      <li>{{lang}}</li>
    </ul>

    </div>

    <div class="flex flex-col">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
          <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-50">
                <tr >
                  <th scope="col" class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Name
                  </th>
                  <th scope="col" class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Programming Language
                  </th>
                  <th scope="col" class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Star Count 
                    <button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortStarsAsc()">Asc</button><button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortStarsDesc()">Desc</button>
                  </th>
                  <th scope="col" class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Fork Count 
                    <button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortForksAsc()">Asc</button><button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortStarsDesc()">Desc</button>
                  </th>
                  <th scope="col" class="relative px-6 py-3">
                    Author Avatar
                  </th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="apis in popularAPIs" v-bind:key="apis.name">
                  <td class="px-6 py-4 whitespace-nowrap">
                        <div class="text-sm font-medium text-gray-900">
                          {{apis.name}}
                        </div>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <div class="text-sm text-gray-500">
                          {{apis.language}}
                    </div>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <div class="text-sm text-gray-900">{{apis.stars}}</div>
                  
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm text-gray-500">{{apis.forks}}</div>
                  </td>            
                  <td class="grid justify-items-center">
                    <img class="author-avatar " :src="apis.avatar">
                  </td>
                
                </tr>

              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
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
