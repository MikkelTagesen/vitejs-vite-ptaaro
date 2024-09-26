<template>
  <div id="app">
    <!-- Main click area -->
    <div @click="handleClick" class="click-area">
      <!-- Loop to generate 6 squares, only when showSquare is true -->
      <div
        v-if="showSquare"
        v-for="(square, index) in 6"
        :key="index"
        class="square"
        :style="{
          top: getSquarePosition(index).top + 'px',
          left: getSquarePosition(index).left + 'px',
        }"
      >
        {{ index + 1 }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showSquare: false, // Boolean to track square visibility
      squarePosition: {
        top: 0,
        left: 0,
      }, // Object to track the position of the original square
      radius: 130, // Radius for the circular placement
    };
  },
  methods: {
    handleClick(event) {
      // Toggle the square's visibility
      this.showSquare = !this.showSquare;

      // Update the square's position to where the cursor clicked only if showing squares
      if (this.showSquare) {
        this.squarePosition = {
          top: event.clientY - 45,
          left: event.clientX - 45,
        };
      }
    },
    getSquarePosition(index) {
      // Calculate angle for each square (60 degrees between each square)
      const angle = (index * 360) / 6; // Divide full circle (360°) into 6 parts
      const angleInRadians = (angle * Math.PI) / 180; // Convert to radians for trigonometry

      // Calculate the top and left position based on the angle and radius
      const top =
        this.squarePosition.top + this.radius * Math.sin(angleInRadians);
      const left =
        this.squarePosition.left + this.radius * Math.cos(angleInRadians);

      return { top, left };
    },
  },
};
</script>

<style>
/* Style for the main click area */
.click-area {
  width: 100vw;
  height: 100vh;
  position: relative;
  background-color: #f0f0f0;
  cursor: pointer;
}

/* Style for the squares */
.square {
  width: 75px;
  height: 75px;
  background-color: pink;
  border-radius: 50%;
  position: absolute; /* Absolutely position the square */
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  font-weight: bold;
}
</style>
