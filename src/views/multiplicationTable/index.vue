<template>
  <div>
    <h1> <span style="cursor: pointer" @click="$router.go(-1)">&lt;</span>&nbsp;&nbsp; 구구단</h1>
  </div>
</template>

<script>
/** *
 * 1. data만 사용할 것
 */
export default {
  name: 'multiplication_table',
  data() {
    return {
    };
  },
};
</script>

<style scoped>

</style>
