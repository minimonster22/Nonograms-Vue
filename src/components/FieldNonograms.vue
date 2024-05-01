<template>
  <div>
    <p>Active Index: {{ activeIndex }}</p>
    <div v-if="activeIndex !== null && solutions[activeIndex]">
      <h2>{{ solutions[activeIndex].name }}</h2>
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
    </div>
    <NameNonograms @update-active-index="handleActiveIndexUpdate" :activeIndex="activeIndex" :name="name"/>
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
.top-wrapper {
  display: flex;
  flex-direction: row;
}

.left-wrapper {
  display: flex;
  flex-direction: column;
}

.top-number {
  display: flex;
  width: 50px;
  height: 109px;
  border-left: 1px solid #E54814;
  border-bottom: 1px solid black;
  flex-direction: column;
  justify-content: end;
  align-items: center;
}

.left-number {
  display: flex;
  width: 67px;
  height: 50px;
  align-self: flex-end;
  border-bottom: 1px solid #E54814;
  border-right: 1px solid black;
}

.empty {
  width: 67px;
}
</style>