<template>
  <b-container>
    <div class="step-wrapper" :class="{ active: isActiveStep }">
      <b-button
        variant="primary"
        @click="nextStep"
        v-if="isFirstStep"
        align-v="end"
      >
        Oda Seçimine İlerle <b-icon icon="forward"></b-icon>
      </b-button>

      <b-button @click="prevStep" v-if="currentstep === 2">
        <b-icon icon="skip-backward"></b-icon> Tarih Seçimine Dön
      </b-button>

      <b-button
        variant="primary"
        @click="nextStep"
        v-if="currentstep === 2"
        align-v="end"
      >
        Ödeme Adımına İlerle <b-icon icon="forward"></b-icon>
      </b-button>

      <b-button @click="prevStep" v-if="isLastStep">
        <b-icon icon="skip-backward"></b-icon> Oda Seçimine Dön
      </b-button>

      <b-button
        variant="success"
        @click="nextStep"
        v-if="isLastStep"
        align-v="end"
      >
        Ödemeyi Tamamla <b-icon icon="check"></b-icon>
      </b-button>
    </div>
  </b-container>
</template>

<script>
export default {
  props: ["step", "stepcount", "currentstep"],
  computed: {
    isActiveStep: function() {
      return this.step.id === this.currentstep;
    },
    isFirstStep: function() {
      return this.currentstep === 1;
    },
    isLastStep: function() {
      return this.currentstep === this.stepcount;
    }
  },
  methods: {
    nextStep: function() {
      this.$emit("step-change", this.currentstep + 1);
    },
    prevStep: function() {
      this.$emit("step-change", this.currentstep - 1);
    }
  }
};
</script>

<style></style>
