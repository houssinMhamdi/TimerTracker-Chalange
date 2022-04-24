<template>
  <div class="container">
    <div class="header">
      <div class="today">
        <span>Today, {{ getdate().day }} </span>
        <span> {{ getdate().name }} </span>
      </div>

      <div class="btns-interactions">
        <div class="btn-stop" @click="$emit('stop')">
          <span>Stop</span>
          <div class="rectangle"></div>
        </div>

        <div class="btn" @click="$emit('start')">
          <span>Start New</span>
          <div class="img"><img src="../assets/timer.svg" alt="timer" /></div>
        </div>
        <h1>{{ timer }}</h1>
      </div>
    </div>

    <div v-for="(lap, index) in laps" :key="index" class="laps">
      <span>Period {{ index + 1 }}:</span>
      <span class="curenttime">
        <div class="started">started</div>
        <div class="br">{{ tim }}</div>
        {{ lap.formattedTime }}
      </span>
    </div>

    <div class="total">
      <span> Total</span>
      <span> 2:55:00 </span>
    </div>
    <div class="line"></div>
  </div>
</template>

<script>
export default {
  name: "TimerTracker",
  props: ["timer", "state", "laps", "tim"],

  methods: {
    getdate() {
      const month = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      const d = new Date();
      let name = month[d.getMonth()];
      let day = d.getDate();
      return { name, day };
    },
  },
  //   total() {
  //     const sum = this.laps.reduce((a, b) => a + b, 0);
  //     console.log(sum);
  //     return sum;
  //   },
};
</script>

<style>
.btn {
  width: 200px;
  height: 38px;
  cursor: pointer;
  display: inline-block;
  line-height: 38px;
  color: #60b669;
  border-radius: 5px;
  border: 1px solid #60b669;
  margin-right: 5px;

  position: relative;
}
.btn span {
  font-weight: 600;
}
.btn-stop {
  width: 120px;
  height: 38px;
  line-height: 38px;
  color: #cc5252;
  border-radius: 5px;
  border: 1px solid #cc5252;
  margin-right: 8px;
  padding-left: 10px;
  position: relative;
  cursor: pointer;
}
.btn-stop span {
  font-weight: 600;
}
.rectangle {
  position: absolute;
  top: 12px;
  left: 10px;
  width: 13px;
  height: 13px;

  background: #cc5252;
}
.header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  border: none;
  width: 80%;
  padding-bottom: 50px;
  margin: auto;
  border-bottom: 1px solid #60b669;
}
.btns-interactions {
  width: 350px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.today span {
  font-weight: 900;
  font-size: 30px;
  color: #415c73;
}
.header h1 {
  font-size: 25px;
  color: #60b669;
  margin-left: 15px;
}
.img {
  width: 13px;
  height: 15px;
  color: #60b669;
  position: absolute;
  top: 2px;
  left: 10px;
}
.laps {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 20px 0;
  border: none;
  border-bottom: 1px solid #60b669;
  width: 80%;
  margin: auto;
}
.laps span {
  font-size: 16px;
  color: #415c73;
  font-weight: 900;
}
.total {
  width: 84.5%;
  margin: auto;
  display: flex;
  justify-content: flex-end;
  margin-left: -150px;
  font-size: 16px;
  color: #6d7783;
  font-weight: 900;
  padding: 50px 0;
}
.total span {
  padding: 15px 0;
  margin-left: 10px;
}
.total span:last-child {
  color: #60b669;
}
.line {
  width: 80%;
  margin: auto;
  height: 1px;
  background: #e8e8e8;
}
.br {
  color: black;
  width: 54px;
  height: 20px;
  font-size: 14px;
  color: #6b7581;
}
.curenttime {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 200px;
}
.started {
  color: #6b7581;
  font-size: 15px;
}
</style>
