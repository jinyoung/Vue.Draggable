<template>

  <draggable tag="ul" :list="tasks" :group="{ name: 'g1' }" handle=".handle">
    <li v-for="(el, idx) in tasks" :key="el.name" class="list-group-item" >

      <i class="fa fa-align-justify handle"></i>

      <input type="text" class="form-control" v-model="el.name"/>

      <i class="fa fa-times close" @click="removeAt(idx)"></i>

      <nested-task  class="dragArea" :tasks="el.tasks"  v-if="el.tasks"/>
    </li>
  </draggable>
</template>
<script>
import draggable from "@/vuedraggable";

export default {
  props: {
    tasks: {
      required: true,
      type: Array
    }
  },
  components: {
    draggable
  },
  methods: {
    removeAt(idx) {
      this.tasks.splice(idx, 1);
    },
  },

  name: "nested-task"
};
</script>
<style scoped>
.dragArea {
  min-height: 50px;
  outline: 1px dashed;
}

.handle {
  float: left;
  padding-top: 8px;
  padding-bottom: 8px;
}

.close {
  float: right;
  padding-top: 8px;
  padding-bottom: 8px;
}

input {
  display: inline-block;
  width: 50%;
}

.text {
  margin: 20px;
}

</style>
