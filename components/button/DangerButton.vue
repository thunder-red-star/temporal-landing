<!-- This DangerButton component extends the BaseButton component -->
<template>
  <BaseButton
      class="primary-button"
      :text="text"
      :disabled="disabled"
      @click="onClick"
      :baseColor="'#ef4760'"
      :accentColor="'#fff'"
      :borderColor="'#ef4760'"
      :doFill="1"
  />
</template>

<script>
import BaseButton from '~/components/button/BaseButton.vue';

export default {
  name: 'DangerButton',
  components: {
    BaseButton
  },
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
    }
  },
  methods: {
    onClick() {
      this.$emit('click')
    }
  },
  mounted() {
    return true;
  },
};
</script>