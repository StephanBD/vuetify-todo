<template>
  <div class="home">
    <!-- <field-add-task /> -->
    <!-- -------------------- -->
    <list-tasks v-if="$store.state.tasks.length" />
    <!-- -------------------- -->
    <no-tasks v-else />
    <button-sorting v-if="$store.state.sorting" />
  </div>
</template>

<script>
// @ is an alias to /src
// import FieldAddTask from "@/components/Todo/FieldAddTask";
// ------
export default {
  name: "Home",
  components: {
    // "field" : FieldAddTask,
    // "field-add-task": require("@/components/Todo/FieldAddTask.vue").default,
    "list-tasks": require("@/components/Todo/ListTasks.vue").default,
    "no-tasks": require("@/components/Todo/NoTasks.vue").default,
    "button-sorting": require("@/components/Todo/ButtonDoneSorting.vue")
      .default,
  },

  methods: {},
};
</script>

<style lang="scss"></style>
