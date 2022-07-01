<template>
  <div @mousemove="move" title="regular tooltip">
    Hover me
    <span>
      {{ currentItem }}
    </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      x: "no",
      y: "no",
    };
  },
  props: {
    currentItem: Object,
  },
  methods: {
    move(event) {
      console.log(event.clientX, event.clientY);
    },
  },
};
</script>

<style>
.tooltip span {
  display: none;
}
.tooltip:hover span {
  display: block;
  position: fixed;
  overflow: hidden;
}
</style>
