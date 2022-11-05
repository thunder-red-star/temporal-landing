<!-- This InfoButton component extends the BaseButton component -->
<template>
  <BaseButton
      class="primary-button"
      :text="text"
      :disabled="disabled"
      @click="onClick"
      :baseColor="'#118ad2'"
      :accentColor="'#fff'"
      :borderColor="'#118ad2'"
      :doFill="1"
  />
</template>

<script>
import BaseButton from '~/components/button/BaseButton.vue';

export default {
  name: 'InfoButton',
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