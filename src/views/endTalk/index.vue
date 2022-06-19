<template>
  <div>
      <h1> <span style="cursor: pointer" @click="$router.go(-1)">&lt;</span>&nbsp;&nbsp; 끝말 잇기</h1>
      <template v-if="state==='play'">
      <div style="display: flex;">
        <h4>
          {{ `점수 : ${score}`}}
        </h4>
        &nbsp;&nbsp;&nbsp;
        &nbsp;&nbsp;&nbsp;
        &nbsp;&nbsp;&nbsp;
        &nbsp;&nbsp;&nbsp;
        <h4>
          {{`시간: ${time}`}}
        </h4>
      </div>
      <div>
        {{this.turn?"사용자 차례":"컴퓨터 차례"}}
      </div>
      <div style="display: flex; align-items: center">
        단어:&nbsp;&nbsp;&nbsp;
        <h4>{{word}}</h4>
      </div>
      <div style="display: flex;">
        <input type="text" v-model="input" ref="text"
               :disabled="!this.turn" @keyup.enter="check">&nbsp;&nbsp;&nbsp;
        <button @click="check">입력</button>
      </div>
      <p v-if="!this.turn">{{this.thinking}}</p>
    </template>
    <template v-else-if="state==='wait'">
      <button @click="restart">게임 시작하기</button>
    </template>
    <template v-else>
      {{this.state==='win'?"사용자 승리":"컴퓨터 승리"}}
      <button @click="restart">다시 하기</button>
    </template>

  </div>
</template>

<script>

export default {
  name: 'end_talk',
  beforeMount() {
    const start = ['강아지', '고양이', '로슈 한계', '이리듐', '김태희', '김예진', '휴대폰', '노트북', '커피', '책상'];
    const num = Math.ceil(Math.random() * 10) - 1;
    this.word = start[num];
    this.timeout = setInterval(() => {
      this.time -= 1;
    }, 1000);
  },
  watch: {
    time(val) {
      if (val <= 0) {
        clearInterval(this.timeout);
        this.time = 0;
        this.state = 'lose';
      }
      if (val === 3 && !this.turn) {
        this.word = this.word[this.word.length - 1]
          + String.fromCharCode(44031 + Math.ceil(11172 * Math.random()));
        this.turn = !this.turn;
      }
    },
    turn(val) {
      clearInterval(this.timeout);
      clearInterval(this.thinkTimeout);
      this.time = 10;
      this.timeout = setInterval(() => {
        this.time -= 1;
      }, 1000);
      if (!val) {
        this.thinkTimeout = setInterval(() => {
          if (this.time !== 10) {
            if (this.time % 3 === 0) {
              this.thinking = '생각하는 중';
            } else {
              this.thinking += '.';
            }
          }
        }, 1000);
      }
      if (val) {
        this.$nextTick(() => {
          this.$refs.text.focus();
        });
      }
    },
  },
  data() {
    return {
      score: 0,
      time: 10,
      word: '',
      input: '',
      state: 'wait',
      timeout: '',
      turn: true,
      thinking: '생각하는 중',
      thinkTimeout: '',
    };
  },
  methods: {
    check() {
      if (!this.turn) {
        alert('사용자의 차례가 아닙니다.!');
      }
      const word = this.word[this.word.length - 1];
      const input = this.input[0];

      this.input = '';
      if (word === input) {
        this.turn = !this.turn;
      }
      if (word !== input) {
        this.state = 'lose';
      }
    },
    restart() {
      const start = ['강아지', '고양이', '로슈 한계', '이리듐', '김태희', '김예진', '휴대폰', '노트북', '커피', '책상'];
      const num = Math.ceil(Math.random() * 10) - 1;
      this.word = start[num];
      this.score = 0;
      this.time = 10;
      this.input = '';
      this.state = 'play';
      this.timeout = '';
      this.turn = true;
      this.$nextTick(() => {
        this.$refs.text.focus();
      });
    },
  },
};
</script>

<style scoped>

</style>
