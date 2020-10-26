<template>
  <div class="container">
    <b-row class="mb-5 mt-5">
      <b-col>
        <b-form-select
          v-model="reservation.room"
          :options="rooms"
        ></b-form-select>
      </b-col>
    </b-row>
    <b-row class="mb-5 mt-5">
      <b-col>
        <b-form-select
          v-model="reservation.roomView"
          :options="roomViews"
        ></b-form-select>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "Step2",
  props: ["reservation"],
  data() {
    return {
      rooms: [
        { value: null, text: "Oda Tipi Seçiniz" },
        "Standart Oda",
        "Deluxe Oda",
        "Suit Oda"
      ],
      roomViews: [
        { value: null, text: "Manzara Seçiniz" },
        "Deniz Manzaralı oda",
        "Kara Manzaralı oda"
      ]
    };
  }
};
</script>

<style></style>
