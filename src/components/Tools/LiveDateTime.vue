<!---------------------------- TEMPLATE ----------->
<template>
  <div class="text-subtitle-1  ml-4">
    {{ date }}
  </div>
</template>
<!----------------------------- SCRIPTS ---------->
<script>
import { format } from "date-fns";
export default {
  name: "",
  // components: {},

  data() {
    return {
      date: "",
    };
  },
  methods: {
    getDate() {
      this.date = format(new Date(), "MMMM d, H:mm:ss");
      setTimeout(this.getDate, 1000);
    },
  },
  mounted() {
    this.getDate();
  },
};
</script>
<!----------------------------- STYLES ---------->
<style scoped lang="scss"></style>
