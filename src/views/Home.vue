<template>
  <div class="home">
    <div v-for="coach in coaches">
      <div class="container">
        <div class="card">
          <div class="card-header">
            <h3>{{coach.name}} </h3>
          </div>
          <div class="card-body">
            <h5 class="card-title">Choose your appointment</h5>
            <p class="card-text">
              <div class="row">
                <div class="col-4" v-for="time_slot in coach.time_slots">
                  <p class="align-center">{{time_slot.day}}:{{time_slot.time_slot}}-{{time_slot.status}}</p>
                  <p class="timezone-text">{{time_slot.timezone}}</p>
                  <p class="align-center"><button v-on:click="timeSlotUpdate(time_slot)" class="btn btn-outline-secondary book-button">Book</button></p>
                </div>
              </div>
            </p>
          </div>
        </div>
        <p></p>
        
      </div>
      <hr>
    </div>
  </div>
</template>

<style>
.timezone-text{
  font-size: 12px;
  color: #747474;
  text-align: center;
}
.align-center{
  text-align: center;
}
.book-button{
  width: 80px;
  height: 40px;
}
</style>

<script>
  import axios from "axios"
  export default {
    data: function () {
      return {
        coaches: [],
        editTimeSlotParams: {}
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
    timeSlotUpdate: function (time_slot) {
      var editTimeSlotParams
      axios.patch("/time_slots/" + time_slot.id, editTimeSlotParams).then((response) => {
        console.log(response);
      })
    },
  },
};
</script>