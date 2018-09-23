<template>
    <div>
        <ul>
            <li v-for="(game,i) in games" v-bind:key="i">{{ game }} - {{ i }}</li>
        </ul>
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
