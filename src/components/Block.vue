<template>
  <div class="block" :style="calcPosition()"  v-show="showBlock" @click="stopTimer">
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
      image: 'assets/monster.jpg',
    }
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true
      this.startTimer()
    }, this.delay)
  },
  methods: {
    startTimer() {
      // start the timer, tick every 10ms
      this.timer = setInterval(() => {
        this.reactionTime += 10
      }, 10)
    },
    stopTimer() {
      // stop the timer
      clearInterval(this.timer);
      this.$emit('end', this.reactionTime)
    },
    calcPosition() {
      return {
        top : (Math.floor(Math.random() * 500)) + 'px',
        left: (Math.floor(Math.random() * 1000)) + 'px'
      }
    }
  }
}
</script>

<style>
  .block {
    background-image: url('../assets/monster.jpg');
    width: 100px;
    border-radius: 20px;
    /* background:  #0faf87; */
    color: white;
    text-align: center;
    padding: 40px 0;
    margin: 40px auto;
    position:absolute;
  }
</style>