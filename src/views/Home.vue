<template>
  <div class="container">
    <step-navigation
      :steps="steps"
      :currentstep="currentstep"
    ></step-navigation>

    <div v-if="isCompleted" class="mt-5 mb-5">
      <b-alert variant="success" show>Rezervasyonunuz tamamlanmıştır.</b-alert>
    </div>

    <b-row
      v-if="reservation.startDate !== null && reservation.endDate !== null"
    >
      <b-col
        >Seçilen Tarihler : {{ reservation.startDate }} /
        {{ reservation.endDate }}
      </b-col>
    </b-row>

    <b-row v-if="reservation.room !== null">
      <b-col>Seçilen Oda : {{ reservation.room }}</b-col>
    </b-row>

    <b-row v-if="reservation.roomView !== null">
      <b-col>Seçilen Manzara : {{ reservation.roomView }}</b-col>
    </b-row>

    <step-1 v-if="currentstep === 1" :reservation="reservation"></step-1>
    <step-2 v-if="currentstep === 2" :reservation="reservation"></step-2>
    <step-3 v-if="currentstep === 3" :card="card"></step-3>

    <step-controls
      v-for="step in steps"
      :key="step.index"
      :step="step"
      :stepcount="steps.length"
      :currentstep="currentstep"
      @step-change="stepChanger"
    >
    </step-controls>
  </div>
</template>

<script>
import StepNavigation from "@/components/StepNavigation.vue";
import StepControls from "@/components/StepControls.vue";

import Step1 from "@/components/Step1.vue";
import Step2 from "@/components/Step2.vue";
import Step3 from "@/components/Step3.vue";

export default {
  components: { StepNavigation, StepControls, Step1, Step2, Step3 },
  data: function() {
    return {
      reservation: {
        startDate: null,
        endDate: null,
        room: null,
        roomView: null
      },
      card: {
        holder: "",
        number: null,
        cvv: null,
        expireMonth: null,
        expireYear: null
      },
      currentstep: 1,
      indicatorclass: true,
      step: 1,
      active: 1,
      firststep: true,
      nextStep: "",
      lastStep: "",
      laststep: false,
      isCompleted: false,
      steps: [
        {
          id: 1,
          title: "Tarih Seçimi",
          icon_class: "calendar-event",
          hasclick: false
        },
        {
          id: 2,
          title: "Oda Seçimi",
          icon_class: "building",
          hasclick: false
        },
        {
          id: 3,
          title: "Ödeme",
          icon_class: "credit-card",
          hasclick: false
        }
      ]
    };
  },
  mounted() {
    if (localStorage.reservation) {
      this.reservation = JSON.parse(localStorage.getItem("reservation"));
    }
  },
  watch: {
    reservation: {
      handler: "saveReservation",
      deep: true
    }
  },
  methods: {
    stepChanger(step) {
      if (this.currentstep === 1) {
        if (this.reservation.startDate === null) {
          alert("Giriş tarihi seçiniz!");
          return;
        }
        if (this.reservation.endDate === null) {
          alert("Çıkış tarihi seçiniz!");
          return;
        }
      }
      if (this.currentstep === 2) {
        if (
          this.reservation.room === null ||
          String(this.reservation.room).trim() === ""
        ) {
          alert("Oda Seçiniz.");
          return;
        }
        if (
          this.reservation.roomView === null ||
          String(this.reservation.roomView).trim() === ""
        ) {
          alert("Manzara Seçiniz.");
          return;
        }
      }
      if (this.currentstep === 3) {
        if (this.card.number === null || String(this.card.number).length < 11) {
          alert("Kart numarasını eksiksiz giriniz!");
          return;
        }
        if (this.card.holder.trim() === "") {
          alert("Kart sahibi giriniz!");
          return;
        }
        if (
          this.card.expireMonth === null ||
          String(this.card.expireMonth).trim() === ""
        ) {
          alert("Son kullanım tarihi ay giriniz!");
          return;
        }
        if (
          this.card.expireYear === null ||
          String(this.card.expireYear).trim() === ""
        ) {
          alert("Son kullanım tarihi yıl giriniz!");
          return;
        }
        if (this.card.cvv === null || String(this.card.cvv).trim() === "") {
          alert("Kredi kartı güvenlik no (cvv) giriniz!");
          return;
        }
        this.isCompleted = true;
        console.log(this.reservation, this.card);
      }
      this.currentstep = step;
    },
    saveReservation() {
      const parsed = JSON.stringify(this.reservation);
      localStorage.setItem("reservation", parsed);
    }
  }
};
</script>

<style></style>
