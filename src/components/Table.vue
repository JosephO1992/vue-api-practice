<template>
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
                        <!-- <button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortStarsAsc()">Asc</button><button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortStarsDesc()">Desc</button> -->
                    </th>
                    <th scope="col" class="px-6 py-3 text-center text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Fork Count 
                        <!-- <button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortForksAsc()">Asc</button><button class="ml-3 py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md shadow-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-opacity-75" v-on:click="sortStarsDesc()">Desc</button> -->
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
</template>
<script>
export default {
    name: 'Table',
    props: {
        popularAPIs: Array
    }
    
}
</script>