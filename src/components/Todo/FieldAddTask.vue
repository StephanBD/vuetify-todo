<!---------------------------- TEMPLATE ----------->
<template>
  <v-text-field
    class="pa-3 fliend-add-task"
    outlined
    placeholder="Add Task"
    hide-details
    clearable
    v-model="newTaskTitle"
    @keyup.enter="addTask"
  >
    <template v-slot:append>
      <v-icon @click="addTask" color="primary" :disabled="newTitleInvalid">
        mdi-plus
      </v-icon>
    </template>
  </v-text-field>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
// import axios from 'axios';
export default {
  name: "FieldAddTask",
  // components: {},
  //	props: [''],
  data() {
    return {
      newTaskTitle: "",
    };
  },
  computed: {
    newTitleInvalid() {
      return !this.newTaskTitle;
    },
  },
  methods: {
    addTask() {
      if (!this.newTitleInvalid) {
        // this.$store.commit("addTask", this.newTaskTitle);
        this.$store.dispatch("addTask", this.newTaskTitle);

        this.newTaskTitle = "";
      }
    },
  },
};
</script>

<style lang="scss">
.fliend-add-task.v-input--is-focused .v-input__slot {
  background: rgba(19, 84, 122, 0.5) !important;
}
</style>
