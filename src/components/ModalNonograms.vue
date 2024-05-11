<template>
  <div class="modal" v-if="show">
    <div class="overlay"></div>
    <div class="modal-content">
      <button @click="close" class="close-btn"><svg class="close-btn-svg" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M6.99486 7.00636C6.60433 7.39689 6.60433 8.03005 6.99486 8.42058L10.58 12.0057L6.99486 15.5909C6.60433 15.9814 6.60433 16.6146 6.99486 17.0051C7.38538 17.3956 8.01855 17.3956 8.40907 17.0051L11.9942 13.4199L15.5794 17.0051C15.9699 17.3956 16.6031 17.3956 16.9936 17.0051C17.3841 16.6146 17.3841 15.9814 16.9936 15.5909L13.4084 12.0057L16.9936 8.42059C17.3841 8.03007 17.3841 7.3969 16.9936 7.00638C16.603 6.61585 15.9699 6.61585 15.5794 7.00638L11.9942 10.5915L8.40907 7.00636C8.01855 6.61584 7.38538 6.61584 6.99486 7.00636Z"></path> </g></svg></button>
      <div class="congratulation">Отлично! Вы решили нонограмму!</div>
      <div class="time-finish">Время, затраченное на решение: </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['show'],
  methods: {
    close() {
      this.$emit('close');
    }
  }
};
</script>

<style scoped>
.modal-content {
  position: absolute;
  width: 25%;
  height: auto;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 25px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;

  font-family: 'Black Ops One', system-ui;
  background-color: #F3F3F3;
  border: 2px solid #E54814;
  border-radius: 38px;

  font-size: 24px;
  text-align: center;
}

.overlay {
  display: block;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.close-btn {
  width: 24px;
  height: 24px;
  align-self: end;
  border: 1px solid #E54814;
  padding: 0;
  cursor: pointer;
  background-color: black;
}
.close-btn-svg {
  width: 22px;
  height: 22px;
  fill: #EFEFEF;

  &:hover {
    fill: #E54814;
  }
}
</style>