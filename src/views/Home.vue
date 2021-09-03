<template>
  <div class="home">
    <p>{{ coaches }}</p>
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