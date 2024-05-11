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
              <div v-for="(cell, cellIndex) in row" :key="cellIndex"
                   :data-id="0"
                   class="cell-board"
                   @click="event => toggleCell(rowIndex, cellIndex, event)"
                   @contextmenu.stop="handleRightClick($event)">
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
    },
    toggleCell(rowIndex, cellIndex, event) {
      const item = event.currentTarget;
      let target = event.target;
      const currentDataId = item.getAttribute('data-id');
      const newDataId = currentDataId === '0' ? '1' : '0';
      item.setAttribute('data-id', newDataId);

      if (target.classList.contains('cross-cell')) {
        item.classList.toggle('black');
        target.remove();
      } else {
        item.classList.toggle('black');
      }

      this.solutions[this.activeIndex].dataField[rowIndex][cellIndex] = parseInt(newDataId);
      const cellDataNew = JSON.parse(localStorage.getItem('cellDataNew'));
      cellDataNew[rowIndex * this.solutions[this.activeIndex].dataField[0].length + cellIndex] = parseInt(newDataId);
      localStorage.setItem('cellDataNew', JSON.stringify(cellDataNew));
    },
    handleRightClick(event) {
      event.preventDefault();
      let item = event.currentTarget;
      let existingCrossCell = item.querySelector('.cross-cell');

      if (existingCrossCell) {
        existingCrossCell.remove();
      } else {
        let crossCell = document.createElement('span');
        crossCell.className = "cross-cell";
        item.appendChild(crossCell);
      }

      if (item.classList.contains('black')) {
        item.classList.remove('black');
      }
    }
  },
  mounted() {
    if (this.activeIndex !== null && this.solutions[this.activeIndex]) {
      // Сохраняем cellData в Local Storage
      const cellData = this.solutions[this.activeIndex].dataField.flat();
      localStorage.setItem('cellData', JSON.stringify(cellData));

      // Создаем новую строку cellDataNew в Local Storage
      const cellDataNew = new Array(this.solutions[this.activeIndex].dataField.length * this.solutions[this.activeIndex].dataField[0].length).fill(0);
      localStorage.setItem('cellDataNew', JSON.stringify(cellDataNew));
    }
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

.black {
  background-color: black;
}
</style>

<style>
.cross-cell {
  display: inline-block;
  width: 100%;
  height: 100%;
  position: relative;

  &:before,
  &:after {
    content: '';
    position: absolute;
    left: 50%;
    width: 2px;
    height: 100%;
    background-color: black;
  }

  &:before {
    transform: rotate(45deg);
  }

  &:after {
    transform: rotate(-45deg);
  }
}
</style>