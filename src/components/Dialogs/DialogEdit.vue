<!---------------------------- TEMPLATE ----------->
<template>
  <v-dialog v-model="dialog" persistent max-width="290">
    <v-card>
      <v-card-title class="headline">
        Edit Task
      </v-card-title>
      <v-card-text>
        Edit the title
      </v-card-text>
      <v-text-field v-model="taskTitle" @keyup.enter="saveTask" />
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn text @click="close">
          Cancel
        </v-btn>
        <v-btn
          color="red darken-1"
          text
          @click="saveTask"
          :disabled="invalidtitle"
        >
          Save
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
      taskTitle: null,
    };
  },
  mounted() {
    this.taskTitle = this.task.title;
  },
  computed: {
    invalidtitle() {
      return !this.taskTitle || this.taskTitle === this.task.title;
    },
  },
  methods: {
    saveTask() {
      if (!this.invalidtitle) {
        let payload = {
          id: this.task.id,
          title: this.taskTitle,
        };
        // console.log(payload);
        this.$store.dispatch("updateTaskTitle", payload);
        this.close();
        this.$vuetify.goTo(0, { duration: 0 });
      }
    },
    close() {
      this.$emit("close");
    },
  },
};
</script>
<!----------------------------- STYLES ---------->
<style scoped lang="scss"></style>
