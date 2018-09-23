<template>
    <div>
        <input type="checkbox" v-model="checked">
        English ??? {{ checked }}
        <div v-if="checked">Hello World</div>
        <div v-else>Bonjour le monde</div>
    </div>
</template>

<script>
  export default {
    data: function () {
      return {
        checked: 'true'
      };
    }
  };
</script>

<style scoped></style>
