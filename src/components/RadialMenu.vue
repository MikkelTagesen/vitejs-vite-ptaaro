<template>
<div
  class="menu"
  :style="{
    left: position.x - 100 + 'px',
    top: position.y - 100 + 'px',
    display: 'flex'
  }"
  @click.stop
>
  <div
    v-for="(item, index) in items"
    :key="item.label"
    class="menu-item"
    :class="item.type"
    :style="{
      left: calculatePosition(index, items.length).x + 100 + 'px',
      top: calculatePosition(index, items.length).y + 100 + 'px'
    }"
    @click="selectItem(item)"
  >
    {{ item.label }}
  </div>
</div>
</template>

<script>
export default {
name: 'RadialMenu',
props: {
  items: Array,
  position: Object
},
methods: {
  calculatePosition(index, totalItems) {
    const radius = 100;
    const angleStep = (2 * Math.PI) / totalItems;
    const angle = index * angleStep;
    const x = Math.cos(angle) * radius;
    const y = Math.sin(angle) * radius;
    return { x, y };
  },
  selectItem(item) {
    alert(`You selected: ${item.label}`);
    this.$emit('closeMenu');
  }
}
};
</script>

<style scoped>
.menu {
position: absolute;
width: 200px;
height: 200px;
border-radius: 50%;
justify-content: center;
align-items: center;
}

.menu-item {
position: absolute;
width: 60px;
height: 60px;
border-radius: 50%;
background-color: lightcoral;
text-align: center;
line-height: 60px;
color: white;
cursor: pointer;
font-weight: bold;
}

/* Color coding */
.breakfast {
background-color: lightblue;
}

.lunch {
background-color: lightgreen;
}

.dinner {
background-color: lightcoral;
}
</style>
