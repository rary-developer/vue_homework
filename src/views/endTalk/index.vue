<template>
  <div>
      <h1> <span style="cursor: pointer" @click="$router.go(-1)">&lt;</span>&nbsp;&nbsp; 끝말 잇기</h1>
  </div>
</template>

<script>
/**
 * 필요하다면 vue의 lifecyclehook을 사용할 것
 * 필요하다면 watch를 사용할 것
 * methods를 사용할 것
 */
export default {
  name: 'end_talk',
  beforeMount() {
  },
  watch: {
  },
  data() {
    return {
    };
  },
  methods: {
  },
};
</script>

<style scoped>

</style>
