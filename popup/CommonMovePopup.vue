<template>
  <div class="common-move-popup transform"
    @mousedown="mousedown"
    ref="movePop"
    :style="{left: left, top: top}" :class="selfClass" v-if="isShow">
    <button type="button" @click="deletePopup" class="delete-button">
      <slot name="delete-crross">
        <span class="delete-pic"></span>
      </slot>
    </button>
    <slot name="title"></slot>
    <slot name='content'></slot>
  </div>
</template>

<script>
  export default {
    name: 'common-move-popup',
    props: {
      value: '',
      selfClass: {
        type: String,
        default: 'defaultClass',
      },
    },
    data () {
      return {
        isShow: false,
        isMouseDown: false,
        startX: '',
        endX: '',
        distanseX: '',
        startY: '',
        endY: '',
        distanseY: '',
        left: '50%',
        top: '50%',
        startLeft: '',
        startTop: '',
      };
    },
    methods: {
      mousedown (e) {
        this.isMouseDown = true;
        this.startX = e.pageX;
        this.startY = e.pageY;
        this.startLeft = this.$refs.movePop.offsetLeft;
        this.startTop = this.$refs.movePop.offsetTop;
      },
      mousemove (e) {
        if (!this.isMouseDown) return false;
        this.endX = e.pageX;
        this.endY = e.pageY;
        this.distanseX = this.endX - this.startX;
        this.distanseY = this.startY - this.endY;
        this.left = this.startLeft + this.distanseX + 'px';
        this.top = this.startTop - this.distanseY + 'px';
      },
      mouseup (e) {
        this.isMouseDown = false;
      },
      deletePopup () {
        this.isShow = false;
        this.$emit('input', this.isShow);
        this.destroy();
      },
      destroy () {
        document.body.removeEventListener('mouseup', this.mouseup);
        document.body.removeEventListener('mousemove', this.mousemove);
      },
    },
    watch: {
      value (val) {
        this.isShow = val;
        if (val) {
          document.body.addEventListener('mouseup', this.mouseup, false);
          document.body.addEventListener('mousemove', this.mousemove, false);
        } else {
          this.destroy();
        }
      },
    },
  };
</script>

<style lang="css" scoped>
  .common-move-popup {
    position: fixed;
  }
  .transform {
    transform: translate(-50%, -50%);
  }
  .defaultClass {
    min-height: 200px;
    border: 1px solid #ccc;
    min-width: 300px;
    font-size: 16px;
    z-index: 2001;
    background-color: #fff;
    border-radius: 8px;
  }
  .delete-button {
    cursor: pointer;
    background-color: transparent;
    width: 1em;
    height: 1em;
    padding: 0;
    margin: 0;
    outline: none;
    border: none;
    position: absolute;
    right: 2px;
    top: 3px;
  }
  .delete-pic {
    position: relative;
    width: 2px;
    height: 1em;
    background: #333;
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);
    -o-transform: rotate(45deg);
    -ms-transform: rotate(45deg);
    transform: rotate(45deg);
    display: inline-block;
  }
  .delete-pic:after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 2px;
    height: 1em;
    background: #333;
    -webkit-transform: rotate(270deg);
    -moz-transform: rotate(270deg);
    -o-transform: rotate(270deg);
    -ms-transform: rotate(270deg);
    transform: rotate(270deg);
  }

</style>
