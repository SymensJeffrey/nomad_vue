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
                  <p class="align-center"><a href="#" class="btn btn-primary">Go somewhere</a></p>
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
</style>

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