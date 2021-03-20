<!---------------------------- TEMPLATE ----------->
<template>
  <v-list flat class="pt-0">
    <!-- <task v-for="task in $store.state.tasks" :key="task.id" :task="task" /> -->
    <!-- :list="$store.getters.taskFiltered" -->

    <draggable handle=".handle" v-model="tasks">
      <task v-for="task in tasks" :key="task.id" :task="task" />
    </draggable>
  </v-list>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
import draggable from "vuedraggable";

export default {
  name: "",
  components: {
    draggable,
    task: require("@/components/Todo/Task").default,
  },
  //	props: [''],
  data() {
    return {};
  },
  computed: {
    tasks: {
      get() {
        return this.$store.getters.taskFiltered;
      },
      set(value) {
        this.$store.dispatch("setTasks", value);
      },
    },
  },
};
</script>
