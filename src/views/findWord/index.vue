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
/**
 * import lyrics from '@/views/findWord/lyrics.json'; 를 사용해서 json을 가져올 것
 * computed를 사용해서 문제를 해결할 것
 */
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
