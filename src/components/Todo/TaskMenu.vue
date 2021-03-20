<!---------------------------- TEMPLATE ----------->
<template>
  <div>
    <v-menu bottom left>
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="primary" icon v-bind="attrs" v-on="on">
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-item
          v-for="(item, index) in items"
          :key="index"
          @click="handleClick(index)"
        >
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <dialog-delete
      v-if="dialogs.delete"
      :task="task"
      @close="dialogs.delete = false"
    />
    <dialog-edit
      v-if="dialogs.edit"
      :task="task"
      @close="dialogs.edit = false"
    />
    <due-date v-if="dialogs.date" :task="task" @close="dialogs.date = false" />
  </div>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
export default {
  components: {
    "dialog-delete": require("@/components/Dialogs/Dialog.vue").default,
    "dialog-edit": require("@/components/Dialogs/DialogEdit.vue").default,
    "due-date": require("@/components/Dialogs/DialogDueDate.vue").default,
  },
  props: ["task"],

  data: () => ({
    dialogs: {
      edit: false,
      delete: false,
      date: false,
    },
    items: [
      {
        title: "Edit",
        icon: "mdi-pencil",
        click() {
          this.dialogs.edit = true;
        },
      },
      {
        title: "Due Date",
        icon: "mdi-calendar",
        click() {
          this.dialogs.date = true;
        },
      },
      {
        title: "Delete",
        icon: "mdi-delete",
        click() {
          this.dialogs.delete = true;
        },
      },
      {
        title: "Sorting",
        icon: "mdi-drag-horizontal-variant",
        click() {
          if (!this.$store.state.search) {
            this.$store.commit("toggleSorting");
          } else {
            this.$store.commit("showSnackbar", "how dare you");
          }
        },
      },
    ],
  }),
  methods: {
    handleClick(index) {
      this.items[index].click.call(this);
    },
  },
};
</script>
<!----------------------------- STYLES ---------->
<style scoped lang="scss"></style>
