<template>
    <div class="container direction">
      <h2>Top 10 Most Popular languages</h2>
        <ul v-for="lang in popularLangs.slice(0,10)" v-bind:key="lang">
          <li>{{lang}}</li>
        </ul>
    </div>
</template>
<script>
export default {
    name: 'List',
    props: {
        popularLangs: Array
    }
}
</script>