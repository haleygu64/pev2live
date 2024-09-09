<template>
  <pev2 :plan-source="planSource" :plan-query="planQuery"></pev2>
</template>

<script>
import { Plan } from "pev2";
export default {
  name: 'Pev2Wrapper',
  components: {
    pev2: Plan,
  },
  props: {
    planSource: {
      type: String,
      required: true,
    },
    planQuery: {
      type: String,
      required: true,
    }
  },
  methods: {
    handleBack() {
      this.$emit('back');
    },
  },
};
</script>
<style lang="scss">
html,
body,
#app {
  height: 100%;
}
</style>