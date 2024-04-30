<template>
  <div ref="wrapper" class="name-wrapper">
    <div v-for="(solution, index) in solutions" :key="index" class="solution-item">
      <p>{{ solution.name }}</p>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      solutions: [
        { name: "Heart" },
        { name: "Eye in dark" },
        { name: "Eye" },
        { name: "Octopus" },
        { name: "Snake" }
      ]
    };
  },
};
</script>

<style scoped>
.name-wrapper {
  display: flex;
  flex-direction: column;
  background-color: #E54814;
  color: #EFEFEF;
  font-family: "Black Ops One", system-ui;
  font-size: 20px;
  font-weight: bold;
  width: fit-content;
  position: absolute;
  top: 5%;
}

.solution-item {
  cursor: pointer;
  padding: 5px;
  text-align: center;
  border: 1px solid black;
}
p {
  margin: 0;
}
.solution-item:hover {
  background-color: black;
}

</style>
