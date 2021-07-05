<template>
  <div id="app">
    <Header/>
    
    <div class="container">
      <h2>Most Popular APIs</h2>
      <table class="apiTable">
        <tr>
          <th>Name</th>
          <th>Programming Language</th>
          <th >Star Count <button v-on:click="sortStarsAsc()">Asc</button><button v-on:click="sortStarsDesc()">Desc</button></th>
          <th >Fork Count <button v-on:click="sortForksAsc()">Asc</button><button v-on:click="sortStarsDesc()">Desc</button></th>
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
    <div class="container direction">
      <h2>Top 10 Most Popular languages</h2>
    <ul v-for="lang in popularLangs.slice(0,10)" v-bind:key="lang">
      <li>{{lang}}</li>
    </ul>

    </div>

    <!-- <div class="flex flex-col">
  <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
    <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
      <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
        <table class="min-w-full divide-y divide-gray-200">
          <thead class="bg-gray-50">
            <tr>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Name
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Title
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Status
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Role
              </th>
              <th scope="col" class="relative px-6 py-3">
                <span class="sr-only">Edit</span>
              </th>
            </tr>
          </thead>
          <tbody class="bg-white divide-y divide-gray-200">
            <tr>
              <td class="px-6 py-4 whitespace-nowrap">
                <div class="flex items-center">
                  <div class="flex-shrink-0 h-10 w-10">
                    <img class="h-10 w-10 rounded-full" src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60" alt="">
                  </div>
                  <div class="ml-4">
                    <div class="text-sm font-medium text-gray-900">
                      Jane Cooper
                    </div>
                    <div class="text-sm text-gray-500">
                      jane.cooper@example.com
                    </div>
                  </div>
                </div>
              </td>
              <td class="px-6 py-4 whitespace-nowrap">
                <div class="text-sm text-gray-900">Regional Paradigm Technician</div>
                <div class="text-sm text-gray-500">Optimization</div>
              </td>
              <td class="px-6 py-4 whitespace-nowrap">
                <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">
                  Active
                </span>
              </td>
              <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                Admin
              </td>
              <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                <a href="#" class="text-indigo-600 hover:text-indigo-900">Edit</a>
              </td>
            </tr>

          </tbody>
        </table>
      </div>
    </div>
  </div>
</div> -->
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
}

.author-avatar {
  width: 100px;
  height: 100px;
}

li {
  list-style: none;
}

</style>
