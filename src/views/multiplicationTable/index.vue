<template>
  <div>
    <h1> <span style="cursor: pointer" @click="$router.go(-1)">&lt;</span>&nbsp;&nbsp; 구구단</h1>
    <div style="display: flex;">
      <input type="nubmer" v-model="dan">&nbsp;단
    </div>
    <table v-if="dan!==''">
      <tr v-for="item in 9" :key="item">
        <td>{{dan}}</td>
        <td>X</td>
        <td>{{item}}</td>
        <td>=</td>
        <td>{{dan*item}}</td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
  name: 'multiplication_table',
  data() {
    return {
      dan: '',
    };
  },
};
</script>

<style scoped>

</style>
