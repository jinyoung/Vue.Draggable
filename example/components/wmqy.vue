<template>
  <div class="row">

          
    <div class="col-3">
      <h3>Y({{sumOfLoadForYear}}/365 - {{fullRatioForYear}}%)</h3>

      <draggable class="list-group" :list="year" group="todo" @change="log">
        <div
          class="list-group-item"
          v-for="(element) in year"
          :key="element.name"
        >
          {{ element.name }} ({{ element.load }})
        </div>
      </draggable>
    </div>

    <div class="col-3">
      <h3>Q({{sumOfLoadForQuarter}}/90)</h3>
      <draggable class="list-group" :list="quarter" group="todo" @change="log">
        <div
          class="list-group-item"
          v-for="(element) in quarter"
          :key="element.name"
        >
          {{ element.name }} ({{ element.load }})
        </div>
      </draggable>
    </div>

    <div class="col-3">
      <h3>M{{sumOfLoadForMonth}}/30</h3>
      <draggable class="list-group" :list="month" group="todo" @change="log">
        <div
          class="list-group-item"
          v-for="(element) in month"
          :key="element.name"
        >
          {{ element.name }} ({{ element.load }})
        </div>
      </draggable>
    </div>

    <div class="col-3">
      <h3>W{{sumOfLoadForWeek}}/7 - {{fullRatioForWeek}}%</h3>
      <draggable class="list-group" :list="week" group="todo" @change="log">
        <div
          class="list-group-item"
          v-for="(element) in week"
          :key="element.name"
        >
          {{ element.name }} ({{ element.load }})
        </div>
      </draggable>
    </div>

    <div class="col-3">
      <h3>Done - {{sumOfLoadForDone}}</h3>
      <draggable class="list-group" :list="done" group="todo" @change="log">
        <div
          class="list-group-item"
          v-for="(element) in done"
          :key="element.name"
        >
          {{ element.name }} ({{ element.load }})
        </div>
      </draggable>
    </div>
    <button class="btn btn-secondary" @click="addYear">Add</button>


    <!-- <rawDisplayer class="col-3" :value="month" title="List 1" />

    <rawDisplayer class="col-3" :value="week" title="List 2" /> -->
  </div>
</template>
<script>
import draggable from "@/vuedraggable";

let id=3;
export default {
  name: "wmqy",
  display: "Wmqy",
  order: 1,
  components: {
    draggable
  },
  data() {
    return {
      year: [
        { name: "Todo 1", load: 1, id: 1 },
        { name: "Todo 2", load: 2, id: 2 },
      ],
      quarter: [
      ],
      month: [
      ],
      week: [
      ],
      done: [
      ],
    };
  },
  computed: {
    sumOfLoadForYear(){
      return this.sum([...this.year, ...this.quarter, ...this.month, ...this.week])
    },
    sumOfLoadForQuarter(){
      return this.sum([...this.quarter, ...this.month, ...this.week])
    },
    sumOfLoadForMonth(){
      return this.sum([ ...this.month, ...this.week])
    },
    sumOfLoadForWeek(){
      return this.sum([ ...this.week])
    },
    sumOfLoadForDone(){
      return this.sum([ ...this.done])
    },

    fullRatioForYear(){
      return (this.sumOfLoadForYear * 100 / 365).toFixed(1)
    },
    fullRatioForQuarter(){
      return (this.sumOfLoadForQuarter * 100 / 90).toFixed(1)
    },
    fullRatioForMonth(){
      return (this.sumOfLoadForMonth * 100 / 30).toFixed(1)
    },
    fullRatioForWeek(){
      return (this.sumOfLoadForWeek * 100 / 7).toFixed(0)
    }

  },
  methods: {
    sum(list){
      return list.reduce((sum, item) => sum + item.load, 0)
    },
    addYear: function() {
      this.year.push({ name: "Todo 1", load: 1, id: id ++ });
    },
    replace: function() {
      this.list = [{ name: "Edgard" }];
    },
    clone: function(el) {
      return {
        name: el.name + " cloned"
      };
    },
    log: function(evt) {
      window.console.log(evt);
    }
  }
};
</script>
