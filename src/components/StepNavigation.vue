<template>
  <ol class="step-indicator">
    <li
      v-for="step in steps"
      is="step-navigation-step"
      :step="step"
      :currentstep="currentstep"
      :key="step.id"
    ></li>
  </ol>
</template>

<script>
import StepNavigationStep from "@/components/StepNavigationStep.vue";

export default {
  props: ["steps", "currentstep"],
  components: { StepNavigationStep },
  data: function() {
    return {
      indicatorclass: false
    };
  }
};
</script>

<style>
.step-wrapper {
  padding: 0;
  display: none;
}

.step-wrapper.active {
  display: block;
}

.step-indicator {
  border-collapse: separate;
  display: table;
  margin-left: 0px;
  position: relative;
  table-layout: fixed;
  text-align: center;
  vertical-align: middle;
  margin-top: 20px;
  padding-top: 0;
  padding-bottom: 10px;
  padding-left: 20%;
  padding-right: 20%;
}

.step-indicator li {
  display: table-cell;
  position: relative;
  float: none;
  padding: 0;
  width: 1%;
}

.step-indicator li:after {
  background-color: #ccc;
  content: "";
  display: block;
  height: 1px;
  position: absolute;
  width: 100%;
  top: 32px;
}

.step-indicator li:after {
  left: 50%;
}

.step-indicator li:last-child:after {
  display: none;
}

.step-indicator li.active .step {
  border-color: #4183d7;
  color: #4183d7;
}

.step-indicator li.active .caption {
  color: #4183d7;
}

.step-indicator li.complete:after {
  background-color: #87d37c;
}

.step-indicator li.complete .step {
  border-color: #87d37c;
  color: #87d37c;
}

.step-indicator li.complete .caption {
  color: #87d37c;
}

.step-indicator .step {
  background-color: #fff;
  border-radius: 50%;
  border: 1px solid #ccc;
  color: #ccc;
  font-size: 20px;
  height: 50px;
  line-height: 50px;
  margin: 0 auto;
  position: relative;
  width: 50px;
  z-index: 1;
}

.step-indicator .step:hover {
  cursor: pointer;
}

.step-indicator .caption {
  color: #ccc;
  padding: 0;
}
</style>
