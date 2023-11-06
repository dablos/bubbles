<template>
  <div
    class="custom-cursor"
    :style="{ left: `${cursorX}px`, top: `${cursorY}px` }"
  ></div>
</template>

<style scoped>
.custom-cursor {
  width: 30px;
  height: 30px;
  border: 2px solid #000;
  border-radius: 50%;
  position: fixed;
  transform: translate(-50%, -50%);
  pointer-events: none;
  z-index: 9999;
}
</style>

<script>
export default {
  name: "CustomCursor",
  data() {
    return {
      cursorX: -100, // Initial position off-screen
      cursorY: -100,
    };
  },
  mounted() {
    window.addEventListener("mousemove", this.updateCursorPosition);
  },
  methods: {
    updateCursorPosition(event) {
      this.cursorX = event.clientX;
      this.cursorY = event.clientY;
    },
  },
  beforeDestroy() {
    window.removeEventListener("mousemove", this.updateCursorPosition);
  },
};
</script>
