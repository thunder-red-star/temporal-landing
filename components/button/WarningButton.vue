<!-- This WarningButton component extends the BaseButton component -->
<template>
  <BaseButton
      class="primary-button"
      :text="text"
      :disabled="disabled"
      @click="onClick"
      :baseColor="'#ffd166'"
      :accentColor="'#fff'"
      :borderColor="'#ffd166'"
      :doFill="1"
  />
</template>

<script>
import BaseButton from '~/components/button/BaseButton.vue';

export default {
  name: 'WarningButton',
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