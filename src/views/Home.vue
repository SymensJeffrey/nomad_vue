<template>
  <div class="home">
    <div v-for="coach in coaches">
      <p> {{coach.name}} </p>
      <div v-for="time_slot in coach.time_slots">
        <p>{{time_slot.day}}:{{time_slot.time_slot}}-{{time_slot.status}}</p>
        <p>{{time_slot.timezone}}</p>
      </div>
      <hr>
    </div>
  </div>
</template>

<style></style>

<script>
  import axios from "axios"
  export default {
    data: function () {
      return {
        coaches: []
      };
    },
    created: function () {
      this.coachesIndex();
    },
    methods: {
      coachesIndex: function(){
        axios.get("/coaches").then((response) => {
        console.log("coaches index", response);
        this.coaches = response.data;
      });
    },
  },
};
</script>