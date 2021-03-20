<!---------------------------- TEMPLATE ----------->
<template>
  <div>
    <!--  -->
    <v-list-item
      @click="doneTask(task.id)"
      :class="{ 'blue lighten-5 ': task.done }"
      class="white"
    >
      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox :input-value="task.done" :ripple="false"></v-checkbox>
        </v-list-item-action>

        <v-list-item-content>
          <v-list-item-title
            :class="{ 'text-decoration-line-through': task.done }"
            >{{ task.title }}</v-list-item-title
          >
        </v-list-item-content>
        <!--  -->
        <v-list-item-action v-if="task.dueDate">
          <v-list-item-action-text>
            <v-icon small>mdi-calendar</v-icon>
            {{ task.dueDate | niceDate }}
          </v-list-item-action-text>
        </v-list-item-action>
        <!--  -->
        <v-list-item-action>
          <task-menu :task="task" />
        </v-list-item-action>
        <!--  -->
        <v-list-item-action v-if="$store.state.sorting">
          <v-btn color="primary" icon class="handle">
            <v-icon>mdi-drag-horizontal-variant</v-icon>
          </v-btn>
        </v-list-item-action>
        <!--  -->
      </template>
    </v-list-item>
    <!--  -->
    <v-divider></v-divider>
  </div>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
import { format } from "date-fns";
export default {
  name: "",
  components: {
    "task-menu": require("@/components/Todo/TaskMenu.vue").default,
  },
  props: ["task"],

  filters: {
    niceDate(value) {
      return format(new Date(value), "MMM d");
    },
  },

  methods: {
    doneTask(id) {
      // let task = this.tasks.filter((task) => task.id === id)[0];
      // task.done = !task.done;
      this.$store.dispatch("doneTask", id);
    },
    deleteTask(id) {
      // this.tasks = this.tasks.filter((task) => task.id !== id);
      this.dialogs.delete = true;
      // this.$store.dispatch("deleteTask", id);
    },
  },
};
</script>

<style lang="scss">
.sortable-gosht {
  opacity: 0;
}
.sortable-drag {
  box-shadow: 0 0 10px rgba($color: #000000, $alpha: 0.3);
}
</style>
