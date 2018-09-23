<template>
    <div class="container">
        <ul class="list-unstyled">
            <li v-for="(game,i) in games" v-bind:key="i">Name : {{ game }} - Index : {{ i }}</li>
        </ul>
        <hr>

        <template v-for="(game,i) in games">
            <h4 v-bind:key="i">Name : {{ game }}</h4>
            <p v-bind:key="i">Index : {{ i }}</p>
        </template>
    </div>
</template>

<script>
  export default {
    data: function () {
      return {
        games: ['Mario', 'Zelda', 'Final Fantasy'],
        support: [
          {
            name: 'Nintendo',
            country: 'JPN',
            type: 'children'
          },
          {
            name: 'Nintendo',
            country: 'JPN',
            type: 'children'
          }
        ]
      };
    }
  };
</script>

<style scoped></style>
