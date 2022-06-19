<template>
  <div>
      <h1>
        <span style="cursor: pointer" @click="$router.go(-1)">
          &lt;
        </span>&nbsp;
        &nbsp; 노래 가사 속 단어 찾기
      </h1>
  </div>
</template>

<script>

export default {
  name: 'find_word',
  data() {
    return {
    };
  },
  computed: {
  },
};
</script>

<style scoped>

</style>
