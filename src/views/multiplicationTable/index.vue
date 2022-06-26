<template>
  <div>
    <h1> <span style="cursor: pointer" @click="$router.go(-1)">&lt;</span>&nbsp;&nbsp; 구구단</h1>
    <div style="display: flex;">
      <div>
        <input type="number" v-model="num">단 <!--숫자 적는 부분-->
      </div>
      <br>
      <div>
        <ul v-if="num !== ''" style="list-style: none"> <!--num에 값이 있을때..-->
          <li v-for="i in 9" :key="i"> <!--i가 9까지 key가 id v-for에 key값 넣기-->
            {{num}} X {{i}} = {{num*i}}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<!--esLint 도대체 뭘까 띄워쓰기 하나 잘못하면 에러를 만들어내네..-->
<script>
export default {
  name: 'multiplication_table',
  data() {
    return {
      num: '',
    };
  },
};
</script>

<style scoped>
</style>
