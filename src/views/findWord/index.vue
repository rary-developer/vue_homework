<template>
  <div>
      <h1>
        <span style="cursor: pointer" @click="$router.go(-1)">
          &lt;
        </span>&nbsp;
        &nbsp; 노래 가사 속 단어 찾기
      </h1>
      <div>
        <input type="text" v-model="word"  >
        <span v-if="count!==0">&nbsp;&nbsp;{{count}} 개의 단어 일치</span>
      </div>
      <pre v-html="lyrics" >

      </pre>
  </div>
</template>

<script>
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
      let temp = lyrics.lyrics;
      if (this.word !== ' ' && this.word !== '') {
      // eslint-disable-next-line no-plusplus
        temp = temp.replaceAll(this.word, `<span style="font-weight:600; color:red;">${this.word}</span>`);
        // eslint-disable-next-line vue/no-side-effects-in-computed-properties
        this.count = temp.split(' ').filter((i) => i.includes(this.word)).length || 0;
      }

      return temp;
    },
  },
};
</script>

<style scoped>

</style>
