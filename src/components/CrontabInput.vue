<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <label for>Hour(s):</label>
        <div class="items">
          <span v-if="hours.length === 0">Every hour</span>
          <span v-for="(v, i) in hours" :key="v">
            <span class="item" @click="handleDel(i, hours)">{{ v }}</span>
          </span>
        </div>
        <select @click="handleAdd($event, hours)">
          <option value>+</option>
          <option v-for="s in 60" :key="s" :value="s-1" v-html="s-1"></option>
        </select>
      </div>

      <div class="col">
        <label for>Minutes(s):</label>
        <div class="items">
          <span v-if="minutes.length === 0">Every minute</span>
          <span v-for="(v, i) in minutes" :key="v">
            <span class="item" @click="handleDel(i, minutes)">{{ v }}</span>
          </span>
        </div>
        <select @click="handleAdd($event, minutes)">
          <option value>+</option>
          <option v-for="s in 60" :key="s" :value="s-1" v-html="s-1"></option>
        </select>
      </div>

      <div class="col">
        <label>Day of week(s):</label>
        <div class="items">
          <span v-if="dow.length === 0">Every day</span>
          <span v-for="(v, i) in dow" :key="v">
            <span class="item" @click="handleDel(i, dow)">{{ daysofweek[v] }}</span>
          </span>
        </div>
        <select @click="handleAdd($event, dow)">
          <option value>+</option>
          <option v-for="(v, i) in daysofweek" :key="i" :value="i" v-html="v"></option>
        </select>
      </div>

      <div class="col">
        <label for>Day of month(s):</label>
        <div class="items">
          <span v-if="dom.length === 0">Any day of month</span>
          <span v-for="(s, i) in dom" :key="s">
            <span class="item" @click="handleDel(i, dom)">{{ s }}</span>
          </span>
        </div>
        <select @click="handleAdd($event, dom)">
          <option value>+</option>
          <option v-for="v in 31" :key="v" :value="v" v-html="v"></option>
        </select>
      </div>

      <div class="col">
        <label>Month(s):</label>
        <div class="items">
          <span v-if="months.length === 0">All months</span>
          <span v-for="(m, i) in months" :key="m">
            <span class="item" @click="handleDel(i, months)">{{ monthsofyear[m] }}</span>
          </span>
        </div>
        <select @click="handleAdd($event, months)">
          <option value>+</option>
          <option v-for="(v, i) in monthsofyear" :key="i" :value="i">{{ i+1 }} {{ v }}</option>
        </select>
      </div>
    </div>

    <div class="info">{{ info }}</div>
  </div>
</template>

<script>
export default {
  props: {
    value: String
  },
  data: function() {
    return {
      hours: [],
      minutes: [0],
      dow: [],
      dom: [],
      months: [],
      monthsofyear: [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
      ],
      daysofweek: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
    };
  },
  methods: {
    handleDel: function(i, array) {
      array.splice(i, 1);
    },
    handleAdd: function(e, array) {
      const i = e.target.value;
      if (i && array.indexOf(i) === -1) {
        array.push(i);
        array.sort((a, b) => a - b);
      }
      e.target.value = "";
    }
  },
  computed: {
    info: function() {
      let h = this.hours.length;
	  h = h === 0 ? 24 : h;
	  
      let m = this.minutes.length;
	  m = m === 0 ? 60 : m;
	  
      let dw = this.dow.length;
	  dw = dw === 0 ? 7 : dw;
	  
      let dm = this.dom.length;
	  dm = dm === 0 ? 31 : dm;
	  
      let my = this.months.length;
	  my = my === 0 ? 12 : my;
	  
      const timesPerDay = h * m;
      const timesPerYear = Math.round(timesPerDay * (dm * my / 7 * dw));

      return (
        timesPerDay +
        " times per day and around " +
        timesPerYear +
        " times per year"
      );
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}
.row {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 10px;
}
.col {
  flex-grow: 1;
  min-width: 9em;
  margin-right: 10px;
  padding: 4px;
  border: 1px solid whitesmoke;
  border-radius: 5px;
}
.col > label {
  display: block;
  border-bottom: 1px solid silver;
  padding: 4px;
  margin: -4px;
}
.col > div {
  padding: 4px;
}
.col > select {
  float: right;
  border: 1px solid silver;
  border-radius: 4px;
  background: whitesmoke;
}
.items {
  font-weight: bold;
  margin-top: 4px;
}
.item {
  display: block;
  text-align: right;
  padding: 0px 6px;
  border-radius: 4px;
  cursor: not-allowed;
  font-weight: bold;
}
.item:hover {
  background-color: lightcoral;
  text-decoration: underline;
}
.info {
    text-align: center;
    font-weight: bold;
}
</style>