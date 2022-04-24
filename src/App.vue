<template>
  <div class="">
    <TimerTracker
      :timer="formattedTime"
      :state="timerState"
      :laps="laps"
      :tim="tim"
      @start="start"
      @lap="lap"
      @stop="stop"
    />
  </div>
</template>

<script>
import TimerTracker from "./components/TimerTracker";
export default {
  name: "App",
  components: { TimerTracker },
  data() {
    return {
      timerState: "stopped",
      currentTimer: 0,
      formattedTime: "00:00:00",
      ticker: undefined,
      laps: [],
      tim: "",
      latestLap: "",
    };
  },

  methods: {
    start() {
      if (this.timerState !== "running") {
        this.tick();
        this.timerState = "running";
      }
        this.tim = this.getTiem();
      
    },
    lap() {
      this.laps.push({
        seconds: this.currentTimer,
        formattedTime: this.formatTime(this.currentTimer),
      });
      this.latestLap = this.formatTime(this.currentTimer);
      this.currentTimer = 0;
    },

    stop() {
      this.laps.push({
        seconds: this.currentTimer,
        formattedTime: this.formatTime(this.currentTimer),
      });
      this.latestLap = this.formatTime(this.currentTimer);
      this.currentTimer = 0;

      window.clearInterval(this.ticker);
      this.currentTimer = 0;
      this.formattedTime = "00:00:00";
      this.timerState = "stopped";
    },
    tick() {
      this.ticker = setInterval(() => {
        this.currentTimer++;
        this.formattedTime = this.formatTime(this.currentTimer);
      }, 250);
    },
    formatTime(seconds) {
      let measuredTime = new Date(null);
      measuredTime.setSeconds(seconds);
      let MHSTime = measuredTime.toISOString().substr(11, 8);
      return MHSTime;
    },
    getTiem() {
      let today = new Date();
      let time =
        today.getHours() + ":" + today.getMinutes();
      return time;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
