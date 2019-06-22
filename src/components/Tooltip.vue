<template>
  <div>
    <slot ref="tooltipSlot"></slot>
    <div
      class="tooltip"
      :class="[`flow-${flow}`, side, hideArrow]"
      :style="{background, maxWidth, padding, top: positioning.top, right: positioning.right, bottom: positioning.bottom, left: positioning.left }"
    >
      <h3 v-show="header">{{header}}</h3>
      {{ msg }}
      <button v-show="linkText" v-html="linkText" @click="tooltipBtnAction"></button>
      <div
        class="arrow"
        :class="side"
        :style="{background: `linear-gradient(45deg, ${background} 50%, rgba(0,0,0,0) 51%)`}"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tooltip",
  props: {
    header: String,
    msg: String,
    linkText: String,
    linkUrl: String,
    background: {
      type: String,
      default: "#333"
    },
    maxWidth: {
      type: String,
      default: "180px"
    },
    padding: {
      type: String,
      default: "10px"
    },
    flow: {
      type: String,
      default: "down"
    },
    side: {
      type: String,
      default: "left"
    },
    position: {
      type: Object,
      default: () => {
        return {
          x: "0px",
          y: "0px"
        };
      }
    },
    showArrow: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    positioning() {
      if (this.side === "left" && this.flow === "up") {
        return {
          top: "initial",
          right: "inital",
          bottom: this.position.y,
          left: this.position.x
        };
      } else if (this.side === "left" && this.flow === "down") {
        return {
          top: this.position.y,
          right: "inital",
          bottom: "initial",
          left: this.position.x
        };
      } else if (this.side === "right" && this.flow === "up") {
        return {
          top: "initial",
          right: this.position.x,
          bottom: this.position.y,
          left: "initial"
        };
      } else if (this.side === "right" && this.flow === "down") {
        return {
          top: this.position.y,
          right: this.position.x,
          bottom: "initial",
          left: "initial"
        };
      }
    },
    hideArrow() {
      if (this.showArrow === false) {
        return "no-arrow";
      }
    }
  },
  methods: {
    tooltipBtnAction() {
      if (this.linkNewWindow) {
      } else {
        window.location = this.linkUrl;
      }
    }
  },
  mounted() {
    this.$refs.tooltipSlot    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.tooltip {
  position: absolute;
  color: #fff;
  font-size: 1rem;
  box-shadow: 2px 2px 10px 2px rgba(0, 0, 0, 0.2);
  &.no-arrow {
    .arrow {
      display: none;
    }
    &.left {
      margin-left: initial;
    }
    &.right {
      margin-right: initial;
    }
  }
  .arrow {
    position: absolute;
    width: 10px;
    height: 10px;
    transform: rotate(45deg);
  }
  &.flow-up .arrow {
    bottom: 20px;
  }
  &.flow-down .arrow {
    top: 20px;
  }
  &.left {
    margin-left: 7px;
    .arrow {
      left: -5px;
    }
  }
  &.right {
    margin-right: 7px;
    .arrow {
      right: -5px;
      transform: rotate(-135deg);
    }
  }
  h3 {
    font-size: 1.2rem;
    margin-top: 0px;
    margin-bottom: 16px;
  }
  button {
    margin-top: 16px;
  }
}
</style>
