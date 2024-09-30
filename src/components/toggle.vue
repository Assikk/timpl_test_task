<template>
  <div class="theme-toggle" @click="isClick = !isClick">
    <div :class="['toggle-button', isClick ? 'right' : 'left']"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isClick: false,
    };
  },
};
</script>

<style scoped>
.theme-toggle {
  width: 54px;
  height: 30px;
  background-color: rgba(142, 108, 234, 0.4);
  border-radius: 25px;
  position: relative;
  cursor: pointer;
}

.toggle-button {
  width: 24px;
  height: 24px;
  background-color: white;
  border-radius: 50%;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  transition: left 0.3s ease;
}

.left {
  left: 2px;
}

.right {
  left: 28px;
}
</style>
