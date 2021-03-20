<!---------------------------- TEMPLATE ----------->
<template>
  <v-text-field
    v-model="$store.state.search"
    @input="$store.commit('setSearch', $event)"
    @focus="searchClosed = false"
    @blur="searchClosed = true"
    :disabled="$store.state.sorting"
    class="mt-1 expanding-search "
    :class="{ closed: searchClosed && !$store.state.search }"
    placeholder="Search"
    prepend-inner-icon="mdi-magnify"
    filled
    dense
    clearable
  ></v-text-field>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
// import axios from 'axios';
export default {
  name: "",
  // components: {},
  //	props: [''],
  data() {
    return {
      searchClosed: true,
    };
  },
  //	methods: {},
};
</script>
<!----------------------------- STYLES ---------->
<style lang="scss">
.expanding-search {
  transition: max-width 0.3s ease-in;
  &.v-input_slot {
    cursor: pointer !important;
    &:before,
    &:after {
      border-color: transparent !important;
    }
  }
  .closed {
    max-width: 45px !important;
    .v-input_slot {
      background: transparent;
    }
  }
}
</style>
