<template>
  <div>
    <p>This is a test paragraph with a button under it</p>
    <PrimaryButton text="Click me" @click="onClick" />
    <SecondaryButton text="Click me" @click="onClick" />
    <SuccessButton text="Click me" @click="onClick" />
    <InfoButton text="Click me" @click="onClick" />
    <WarningButton text="Click me" @click="onClick" />
    <DangerButton text="Click me" @click="onClick" />
  </div>
</template>

<script>
import PrimaryButton from "../components/button/PrimaryButton";
import SecondaryButton from "../components/button/SecondaryButton";
import SuccessButton from "../components/button/SuccessButton";
import WarningButton from "../components/button/WarningButton";
import DangerButton from "../components/button/DangerButton";
import InfoButton from "../components/button/InfoButton";

export default {
  components: {
    WarningButton,
    PrimaryButton,
    SecondaryButton,
    SuccessButton,
    DangerButton,
    InfoButton
  },
  methods: {
    onClick() {
      console.log('Clicked!');
    }
  }
};
</script>