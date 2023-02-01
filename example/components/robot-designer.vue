<template>
  <div class="row">
    <div class="col-3">
      <h3>Draggable 1</h3>
      <draggable
        class="dragArea list-group"
        :list="list1"
        :group="{ name: 'g1', pull: 'clone', put: false }"
        :clone="cloneTask"
        @change="log"
      >
        <div class="list-group-item" v-for="element in list1" :key="element.id">
          {{ element.name }}
        </div>
      </draggable>
    </div>

    <div class="col-3">
      <h3>Draggable 2</h3>

        <nested-draggable :tasks="list2" />

      <!-- <draggable
        class="dragArea list-group"
        :list="list2"
        group="task"
        @change="log"
      >
        <div class="list-group-item" v-for="element in list2" :key="element.id">
          {{ element.name }}
        </div>
      </draggable> -->


    </div>

    <rawDisplayer class="col-3" :value="list1" title="List 1" />

    <rawDisplayer class="col-3" :value="list2" title="List 2" />
  </div>
</template>

<script>
import draggable from "@/vuedraggable";
import nestedDraggable from "./infra/nested";

let idGlobal = 1;
export default {
  name: "robot-designer",
  display: "Robot Designer",
  order: 3,
  components: {
    draggable,
    nestedDraggable
  },
  data() {
    return {
      list1: [
        { name: "For", type: "For", id: 1, tasks: [] },
        { name: "If", type: "If", id: 2, tasks: [] },
        { name: "Task", type: "Task", id: 3 },
      ],
      list2: [
        {
          name: "task 1",
          tasks: [
            {
              name: "task 2",
              tasks: []
            }
          ]
        },
      ]

    };
  },
  methods: {
    log: function(evt) {
      window.console.log(evt);
    },
    cloneTask({ id, type, tasks }) {
      return {
        id: idGlobal++,
        name: `${type} ${id}`,
        type: type,
        tasks: tasks
      };
    }
  }
};
</script>
<style scoped></style>
