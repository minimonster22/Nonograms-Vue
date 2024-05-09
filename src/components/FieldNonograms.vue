<template>
  <div class="inside">
    <NameNonograms @update-active-index="handleActiveIndexUpdate" :activeIndex="activeIndex" :name="name"/>
    <div v-if="activeIndex !== null && solutions[activeIndex]">
      <h2>{{ solutions[activeIndex].name }}</h2>
      <div class="main-wrapper">
        <div class="top-wrapper">
          <div class="top-wrapper empty"></div>
          <div v-for="(array, i) in solutions[activeIndex].numbersTopArray" :key="i">
            <div v-if="Array.isArray(array) && array.length === 1" class="top-number">
              <div>{{ array[0] }}</div>
            </div>
            <div v-else class="top-number double">
              <div v-for="(number, j) in array" :key="j">
                {{ number }}
              </div>
            </div>
          </div>
        </div>
        <div class="board-wrapper">
          <div class="left-wrapper">
            <div v-for="(array, i) in solutions[activeIndex].numbersLeftArray" :key="i">
              <div v-if="Array.isArray(array) && array.length === 1" class="left-number">
                <div>{{ array[0] }}</div>
              </div>
              <div v-else class="left-number double">
                <div v-for="(number, j) in array" :key="j">
                  {{ number }}
                </div>
              </div>
            </div>
          </div>
          <div class="nonogram-board">
            <div v-for="(row, rowIndex) in solutions[activeIndex].dataField" :key="rowIndex" class="row-board">
              <div v-for="(cell, cellIndex) in row" :key="cellIndex" :data-id="cell" class="cell-board">
              </div>
            </div>
          </div>
        </div>
      </div>
      <p>Active Index: {{ activeIndex }}</p>
    </div>
  </div>
</template>

<script>

import solutions from '@/assets/data/solutions.json';
import NameNonograms from "@/components/NameNonograms.vue";

export default {
  props: ['name'],
  data() {
    return {
      solutions: solutions,
      numbersTopArray: solutions,
      activeIndex: 1,
      numbersLeftArray: solutions,
      dataField: solutions
    };
  },
  components: {
    NameNonograms
  },
  methods: {
    handleActiveIndexUpdate(index) {
      console.log('Active index updated in parent:', index);
      this.activeIndex = index;
    }
  },
  mounted() {
    console.log('Active Index:', this.activeIndex);
  }
};
</script>

<style scoped>
.main-wrapper {
  border-width: 3px 2px 2px 3px;
  border-style: solid;
  border-color: #E54814;
  margin-top: 50px;
}

.top-wrapper {
  display: flex;
  flex-direction: row;
}

.top-wrapper > div:nth-child(n+2) {
  border-bottom: 2px solid black;
}

.left-wrapper {
  width: 67px;
  display: flex;
  flex-direction: column;
  border-right: 2px solid black;
}

.top-number {
  display: flex;
  width: 50px;
  height: 109px;
  border-left: 1px solid #E54814;
  flex-direction: column;
  justify-content: end;
  align-items: center;
  font-family: "Black Ops One", system-ui;
  font-size: 27px;
  font-weight: bold;
  color: #333;
}

.left-number {
  display: flex;
  width: 57px;
  height: 50px;
  justify-content: flex-end;
  border-bottom: 1px solid #E54814;
  border-right: 1px solid black;
  font-family: "Black Ops One", system-ui;
  font-size: 27px;
  font-weight: bold;
  color: #333;
  align-items: center;
  padding-left: 5px;
  padding-right: 5px;
}

.empty {
  width: 68px;
  border-bottom: 1px solid #E54814;
}

.inside {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.double {
  gap: 5px;
}

.row-board {
  display: flex;
  flex-direction: row;
}

.cell-board {
  width: 50px;
  height: 50px;
  border-right: 1px solid black;
  border-bottom: 1px solid black;
  background-color: white;
  cursor: pointer;
}

.board-wrapper {
  display: flex;
}

</style>