<template>
  <div>
      <h1>
        <span style="cursor: pointer" @click="$router.go(-1)">
          &lt;
        </span>&nbsp;
        &nbsp; 노래 가사 속 단어 찾기
      </h1>
      <div>
        <input type="text" v-model="word"> <!--검색용 input-->
        <span >{{count}} 개의 단어 일치!</span>
      </div>
    <!-- 템플릿 문법 참조 https://kr.vuejs.org/v2/guide/syntax.html -->
      <p v-html="lyrics">

      </p>
  </div>
</template>

<script>
/**
 * import lyrics from '@/views/findWord/lyrics.json'; 를 사용해서 json을 가져올 것
 * computed를 사용해서 문제를 해결할 것
 */
import lyrics from '@/views/findWord/lyrics.json';

export default {
  name: 'find_word',
  data() {
    return {
      word: '',
      count: 0,
    };
  },
  computed: {
    lyrics() {
      let rtn = lyrics.lyrics;
      if (this.word !== '' && this.word !== '') {
        let rtnArr = rtn.split(' ');
        this.count = rtnArr.filter((i) => i.includes(this.word)).length;
        rtn = rtn.replaceAll(this.word, `<span style="color:red">${this.word}</span>`);
      } else {
        this.count = 0;
      }
      return rtn;
    },
  },
};
</script>

<style scoped>

</style>
