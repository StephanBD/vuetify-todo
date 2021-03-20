<!---------------------------- TEMPLATE ----------->
<template>
  <v-dialog
    ref="dialog"
    :value="true"
    :return-value.sync="date"
    persistent
    width="290px"
  >
    <v-date-picker v-model="date" scrollable>
      <v-spacer></v-spacer>
      <v-btn text color="primary" @click="close">
        Cancel
      </v-btn>
      <v-btn text color="primary" @click="saveTask">
        OK
      </v-btn>
    </v-date-picker>
  </v-dialog>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
// import axios from 'axios';
export default {
  name: "",
  // components: {},
  props: ["task"],
  data() {
    return {
      date: null,
    };
  },
  mounted() {
    if (this.task.dueDate) {
      this.date = this.task.dueDate;
    }
  },
  methods: {
    saveTask() {
      let payload = {
        id: this.task.id,
        dueDate: this.date,
      };
      this.$store.dispatch("updateTaskDueDate", payload);
      this.close();
    },
    close() {
      this.$emit("close");
    },
  },
};
</script>
<!----------------------------- STYLES ---------->
<style scoped lang="scss"></style>
