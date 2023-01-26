<template>
  <div class="dialog" v-if="show" @click.stop="hideDialog">
    <img class="close_svg" @click.stop="hideDialog" src="@/assets/icons/Close_modal.svg" alt="close-modal">
    <div @click.stop class="dialog__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'dialog-window',
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideDialog () {
      this.$emit('show')
    }
  }
}
</script>

<style scoped>
.dialog {
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}

.close_svg {
  position: absolute;
  width: 24px;
  right: 2%;
  top: 2%;
  height: 24px;
}
.close_svg:hover {
  cursor: pointer;
  transform: scaleX(1.2) scaleY(1.2) ;
}
.dialog__content {
  margin: auto;
  border-radius: 12px;
  min-height: 50px;
  min-width: 300px;
}
</style>
