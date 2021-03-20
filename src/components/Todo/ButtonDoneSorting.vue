<!---------------------------- TEMPLATE ----------->
<template>
  <v-btn
    @click="$store.commit('toggleSorting')"
    color="primary"
    class="button-sorting"
  >
    Done Sorting
  </v-btn>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
// import axios from 'axios';
export default {
  name: "",
  // components: {},
  //	props: [''],
  data() {
    return {};
  },
  //	methods: {},
};
</script>
<!----------------------------- STYLES ---------->
<style scoped lang="scss">
.button-sorting {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
}
</style>
