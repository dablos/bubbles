<template>
  <div class="mouse-trail-container" @mousemove="addCircle">
    <CustomCursor v-if="showCursor" />
    <div
      v-for="circle in circles"
      :key="circle.id"
      class="circle"
      :style="circle.style"
    ></div>
  </div>
</template>

<script>
import CustomCursor from "./components/CustomCursor.vue";

export default {
  components: {
    CustomCursor,
  },
  data() {
    return {
      circles: [],
      showCursor: false,
    };
  },
  methods: {
    addCircle(event) {
      const { x, y } = event;
      const delay = this.circles.length * 100;

      this.circles.push({
        id: Date.now(),
        style: {
          left: x + "px",
          top: y + "px",
          opacity: 1,
        },
      });

      if (this.circles.length > 5) {
        const removedCircle = this.circles.shift();
        setTimeout(() => {
          removedCircle.style.opacity = 0;
        }, delay);
      }
    },
  },
};
</script>

<style>
body {
  cursor: none;
}

.mouse-trail-container {
  position: relative;
  width: 100%;
  height: 100vh;
}

.circle {
  position: absolute;
  width: 20px;
  height: 20px;
  border: 2px solid #000;
  border-radius: 50%;
  transition: opacity 0.5s ease;
}
</style>
