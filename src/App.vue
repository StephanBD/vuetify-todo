<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app :mobile-breakpoint="768">
      <v-img
        src="mountains.jpg"
        class="pa-4 pt-7"
        height="170"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar>
          <img
            src="https://cdn.vuetifyjs.com/images/john.jpg"
            alt="John"
            size="70"
            class="mb-2"
          />
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Danny Connell
        </div>
        <div class="white--text text-subtitle-2">Danny_Connell</div>
      </v-img>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link :to="item.to">
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <!-- -------- -->
    <v-app-bar
      color="primary"
      dark
      src="mountains.jpg"
      app
      prominent
      :height="$route.path === '/' ? '230' : '170'"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>
      <!-- ------ -->
      <v-container class="pa-0 mx-0 header-container">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <!--  -->
        <v-row>
          <v-app-bar-title class="ml-4 text-h4">
            {{ $store.state.appTitle }}
          </v-app-bar-title>
        </v-row>
        <!--  -->
        <v-row>
          <live-date />
        </v-row>
        <!--  -->
        <v-row v-if="$route.path === '/'">
          <field-add-task />
        </v-row>
      </v-container>
      <!-- ------ -->
    </v-app-bar>
    <!-- ------------- -->
    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
export default {
  components: {
    snackbar: require("@/components/Shared/Snackbar.vue").default,
    search: require("@/components/Tools/Search.vue").default,
    "live-date": require("@/components/Tools/LiveDateTime.vue").default,
    "field-add-task": require("@/components/Todo/FieldAddTask.vue").default,
  },
  data: () => ({
    drawer: null,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
  }),
  mounted() {
    this.$store.dispatch("getTasks");
  },
};
</script>

<style lang="scss">
.header-container {
  max-width: none !important;
}
</style>
