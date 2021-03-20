<!---------------------------- TEMPLATE ----------->
<template>
  <v-dialog v-model="dialog" persistent max-width="290">
    <v-card>
      <v-card-title class="headline">
        Delete Task?
      </v-card-title>
      <v-card-text>Are you sure you wanna delete it?</v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn text @click="close">
          Disagree
        </v-btn>
        <v-btn color="red darken-1" text @click="deleteTask">
          Agree
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
export default {
  props: ["task"],
  data() {
    return {
      dialog: true,
    };
  },
  methods: {
    close() {
      this.$emit("close");
    },
    deleteTask() {
      // this.tasks = this.tasks.filter((task) => task.id !== id);
      this.$store.dispatch("deleteTask", this.task.id);
      // this.dialog = false;
    },
  },
};
</script>
<!----------------------------- STYLES ---------->
<style scoped lang="scss"></style>
