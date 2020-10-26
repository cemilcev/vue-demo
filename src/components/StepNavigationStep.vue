<template>
  <li :class="indicatorclass">
    <div class="step"><b-icon :icon="step.icon_class"></b-icon></div>
    <div class="caption hidden-xs hidden-sm">
      {{ step.id }}: {{ step.title }}
    </div>
  </li>
</template>

<script>
export default {
  name: "StepNavigationStep",
  props: ["step", "currentstep"],
  computed: {
    indicatorclass: function() {
      return {
        active: this.step.id == this.currentstep,
        hasclick: this.currentstep >= this.step.id,
        complete: this.currentstep > this.step.id
      };
    }
  }
};
</script>

<style></style>
