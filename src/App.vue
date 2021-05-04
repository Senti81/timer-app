<template>
  <v-app>
    <v-content>
      <Timer
        :timer="formattedTime"
        :state="timerState"
        @start="start"
        @pause="pause"
        @stop="stop"
      />
    </v-content>
  </v-app>
</template>

<script>
import Timer from '@/components/Timer';

export default {
  name: 'App',
  components: {
    Timer
  },
  data () {
    return {
      timerState: 'stopped',
      currentTimer: 0,
      endTimerInMinutes: 45,
      formattedTime: "00:00",
      ticker: undefined,
    }
  },
  methods: {
    start () {
      if (this.currentTimer == this.endTimerInMinutes*60*2) {
        window.clearInterval(this.ticker);
        this.currentTimer = 0;
        this.formattedTime = "00:00";
      }
      if (this.timerState !== 'running') {
        this.tick();
        this.timerState = 'running';
      }
    },
    pause () {
      window.clearInterval(this.ticker);
      this.timerState = 'paused';
    },
    stop () {
      window.clearInterval(this.ticker)
      this.currentTimer = 0;
      this.formattedTime = "00:00";
      this.timerState = "stopped";
    },
    tick () {      
      this.ticker = setInterval(() => {
        this.currentTimer++;
        if (this.currentTimer === this.endTimerInMinutes*60 || this.currentTimer === this.endTimerInMinutes*60*2) {
          this.pause()
        }
        this.formattedTime = this.formatTime(this.currentTimer);
        }, 1000)
    },
    formatTime (seconds) {
      let m = Math.floor(seconds / 60);
      let s = seconds % 60;
      return (m < 10 ? "0" + m : m) + ":" + (s < 10 ? "0" + s : s);
    }
  }
}
</script>
