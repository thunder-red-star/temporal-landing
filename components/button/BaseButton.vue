<template>
  <button
      class="button"
      @click="onClick"
      v-bind:disabled="disabled"
      :style="styles"
  >
    <div class="button-inner">
      <div class="button-text">{{ text }}</div>
      <svg class="hover-arrow" width="10" height="10" viewBox="0 0 10 10" aria-hidden="true">
        <g fill-rule="evenodd">
          <path class="hover-arrow-line-path" d="M0 5h7"></path>
          <path class="hover-arrow-tip-path" d="M1 1l4 4-4 4"></path>
        </g>
      </svg>
    </div>
  </button>
</template>

<script>
export default {
  name: 'BaseButton',
  props: {
    text: {
      type: String,
      required: true
    },
    disabled: {
      type: Boolean,
      default: false
    },
    onClick: {
      type: Function,
      required: true
    },
    baseColor: {
      type: String,
      default: '#000'
    },
    accentColor: {
      type: String,
      default: '#fff'
    },
    borderColor: {
      type: String,
      default: '#000'
    },
    doFill: {
      type: Number,
      default: 1
    }
  },
  methods: {
    onClick() {
      this.$emit('click')
    },
    invertColor(hex, bw) {
      if (hex.indexOf('#') === 0) {
        hex = hex.slice(1);
      }
      // convert 3-digit hex to 6-digits.
      if (hex.length === 3) {
        hex = hex[0] + hex[0] + hex[1] + hex[1] + hex[2] + hex[2];
      }
      if (hex.length !== 6) {
        throw new Error('Invalid HEX color.');
      }
      let r = parseInt(hex.slice(0, 2), 16),
        g = parseInt(hex.slice(2, 4), 16),
        b = parseInt(hex.slice(4, 6), 16);
      if (bw) {
        // http://stackoverflow.com/a/3943023/112731
        return (r * 0.299 + g * 0.587 + b * 0.114) > 186
          ? '#000000'
          : '#FFFFFF';
      }
      // invert color components
      r = (255 - r).toString(16);
      g = (255 - g).toString(16);
      b = (255 - b).toString(16);
      // pad each with zeros and return
      return "#" + this.padZero(r) + this.padZero(g) + this.padZero(b);
    },
    padZero(str, len) {
      len = len || 2;
      let zeros = new Array(len).join('0');
      return (zeros + str).slice(-len);
    }
  },
  mounted() {
    return true;
  },
  data() {
    return {
      // Find the inverse of each provided color
      inverseBaseColor: this.invertColor(this.baseColor),
      inverseAccentColor: this.invertColor(this.accentColor),
      inverseBorderColor: this.invertColor(this.borderColor),
    }
  },
};
</script>

<style scoped lang="scss">
.button {
  border: 2px solid v-bind(borderColor);
  border-radius: 50vh;
  padding: 0.25rem 0.7rem;
  font-weight: 600;
  cursor: pointer;
  font-size: 0.8rem;
  transition: all 0.2s ease-in-out;
  position: relative;
  background-color: transparent;
  font-family: 'Open Sauce Sans', 'Inter', 'Ubuntu', 'Helvetica Neue', 'Segoe UI', 'Helvetica', 'Arial', sans-serif;
  overflow: hidden;
  color: v-bind(accentColor);

  &:hover {
    --hover-displace: 3px;
    --hover-opacity: 1;
    --arrow-color: v-bind(accentColor);
  }

  &:active {
    transform: translateY(2px);
  }

  &:after {
    content: '';
    position: absolute;
    top: 0%;
    left: 0;
    width: 0%;
    height: 100%;
    background-color: v-bind(inverseBaseColor);
    /* Calculate opacity based on doFill prop */
    opacity: v-bind(doFill);
    transform: translateX(-100%);
    transition: all 0.2s ease-in-out;
    z-index: -1;
    filter: invert(1);
  }

  &:before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: v-bind(accentColor);
    opacity: 1;
    transition: all 0.2s ease-out;
    z-index: -2;
    border-radius: 50vh;
  }

  &:hover:after {
    width: calc(100% + 4px);
    left: calc(100% + 2px);
    opacity: v-bind(doFill);
  }

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
}

.hover-arrow-tip-path {
  stroke-width: 2;
  fill: none;
  margin-left: 0.5rem;
  transform: translateX(var(--hover-displace, 0));
  transition: all 0.2s cubic-bezier(0.7, 0, 0, 0.7);
}

.hover-arrow-line-path {
  stroke-width: 2;
  fill: none;
  transition: all 0.2s cubic-bezier(0.7, 0, 0, 0.7);
  opacity: var(--hover-opacity, 0);
  stroke: v-bind(inverseBaseColor);
  mix-blend-mode: difference;
}

.hover-arrow {
  display: inline-block;
  vertical-align: middle;
  transform: translateY(-0.5px) translateX(2px);
  transition: transform 0.2s ease-out;
  stroke: v-bind(inverseBaseColor);
  mix-blend-mode: difference;
}

.button-inner {
}

.button-text {
  display: inline-block;
  margin-right: 0.25rem;
  color: v-bind(baseColor);
  mix-blend-mode: difference;
  filter: invert(1);
}
</style>