<template>
    <div>
        <input type="checkbox" v-model="checked">
        English ??? {{ checked }}
        <div v-if="checked">Hello World</div>
        <div v-else>Bonjour le monde</div>
        <p v-show="checked">In the template</p>
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
