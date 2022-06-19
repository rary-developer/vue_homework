<template>
  <div>
    <h1> <span style="cursor: pointer" @click="$router.go(-1)">&lt;</span>&nbsp;&nbsp; 숫자 야구</h1>
    <template v-if="state==='wait'">
      <button @click="changeState">시작하기</button>
    </template>
    <template v-else-if="state==='win'||state==='lose'">
      <p>{{state==='win'?"승리했습니다!":"패배했습니다"}}</p>
      <button @click="changeState">다시하기</button>
    </template>
    <template v-else>
      <p>{{msg}}</p>
      <template v-if="!msg.includes('숫자 선정 중')">
        <p>{{`${count} 회`}}</p>
        <input type="text" v-model="input">
        &nbsp;&nbsp;&nbsp;
        <button @click="check">입력</button>
      </template>

    </template>
  </div>
</template>

<script>
export default {
  name: 'number_baseball',
  data() {
    return {
      state: 'wait',
      solution: '',
      input: '',
      count: '',
      msg: '',
      ballCount: 0,
      outCount: 0,
      strikeCount: 0,
    };
  },
  watch: {
    count(val) {
      if (val > 10) {
        this.state = 'lose';
      }
    },
  },
  methods: {
    changeState() {
      this.state = 'play';
      this.solution = '';
      this.input = '';
      this.count = 1;
      this.msg = '숫자 선정 중';
      let count = 0;
      const timeout = setInterval(() => {
        count += 1;
        this.msg += '.';
        if (count === 3) {
          const set = new Set();
          while (set.size !== 3) {
            set.add(Math.ceil(Math.random() * 9));
          }
          this.solution = Array.from(set);
          this.msg = '';
          clearTimeout(timeout);
        }
      }, 1000);
    },
    check() {
      this.ballCount = 0;
      this.outCount = 0;
      this.strikeCount = 0;
      const { solution } = this;
      const input = this.input.split('');
      this.input = '';
      solution.forEach((sV, sI) => {
        let out = 0;
        input.forEach((iV, iI) => {
          console.log(sV, sI, iV, iI);
          if (sV === Number(iV) && sI !== iI) {
            this.ballCount += 1;
            return false;
          }
          if (sV === Number(iV) && sI === iI) {
            this.strikeCount += 1;
            return false;
          }
          out += 1;
          return false;
        });
        this.outCount += Math.floor(out / 3);
      });

      this.count += 1;
      this.msg = `${this.strikeCount > 0 ? `${this.strikeCount} 스트라이크 ` : ''}
      ${this.ballCount > 0 ? `${this.ballCount} 볼 ` : ''}
      ${this.outCount > 0 ? `${this.outCount} 아웃 ` : ''}`;

      if (this.strikeCount === 3) {
        this.state = 'win';
      }
    },
  },
};
</script>

<style scoped>

</style>
