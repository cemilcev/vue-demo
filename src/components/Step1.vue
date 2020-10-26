<template>
  <div class="container">
    <b-row class="mb-5 mt-5" align-v="center">
      <b-col>
        <b-form-datepicker
          id="start-date"
          v-model="reservation.startDate"
          locale="tr"
          :hide-header="true"
          class="mb-2"
          placeholder="Giriş Tarihi Seçiniz"
        ></b-form-datepicker>
      </b-col>
      <b-col>
        <b-form-datepicker
          id="end-date"
          v-model="reservation.endDate"
          locale="tr"
          :hide-header="true"
          class="mb-2"
          placeholder="Çıkış Tarihi Seçiniz"
        ></b-form-datepicker>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "Step1",
  props: ["reservation"]
};
</script>
