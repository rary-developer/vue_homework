<template>
  <div>
    <h1><span style="cursor: pointer" @click="$router.go(-1)">&lt;</span>&nbsp;&nbsp; 신호등</h1>
    <div class="container">
      <span class="lights" :class="{red:light==='red'}"></span>
      <span class="lights" :class="{yellow:light==='yellow'}"></span>
      <span class="lights" :class="{green:light==='green'}"></span>
    </div>
    <div class="pannel">
      <button @click="flash('red')">빨간불</button>
      <button @click="flash('yellow')">노란불</button>
      <button @click="flash('green')">초록불</button>
      <button @click="flash('auto')">자동</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'traffic_light',
  data() {
    return {
      light: '',
    };
  },
  methods: {
    flash(light) {
      if (light === 'auto') {
        setTimeout(() => {
          this.light = 'yellow';
          setTimeout(() => {
            this.light = 'green';
          }, 2000);
        }, 3000);
        this.light = 'red';
        return false;
      }
      this.light = light;
      return false;
    },
  },
};
</script>

<style scoped>
.pannel{
  width: 300px;
  height: 100px;
  display:flex;
  justify-content: space-around;
  align-items: center;
}
.container{
  border: black 1px solid;
  width: 300px;
  height: 100px;
  display:flex;
  justify-content: space-around;
  align-items: center;
}
  .lights{
    border: none;
    border-radius: 100%;
    background-color: gray;
    display: inline-block;
    width: 80px;
    height: 80px;
  }
  .red{
    background-color: red;
  }
  .yellow{
    background-color: yellow;
  }
  .green{
    background-color: green;
  }
</style>
