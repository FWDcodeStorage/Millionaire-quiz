<template>
  <div class="container welcome">
    <h1>Welcome {{ name }}</h1>
    <p>
      Lorem ipsum, dolor sit amet consectetur adipisicing elit. Qui provident
      sint voluptatum aliquid soluta ipsam fugit nulla. Laborum, sed
      accusantium?
    </p>
    <div class="btns">
      <button @click.prevent="handleBack">Back</button>
      <button @click.prevent="handlePlay">Play</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["name"],
  methods: {
    handleBack() {
      this.$emit("goTo", 0);
    },
    handlePlay() {
      this.$emit("goTo", 2);
    },
  },
};
</script>

<style lang="scss">
.welcome {
  h1 {
    margin-bottom: 1.5rem;
  }
  p {
    font-size: 16px;
    letter-spacing: 1px;
    color: #8c8c8c;
    margin-bottom: 1.5rem;
  }
  .btns {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;

    button {
      width: 200px;
    }
  }
}
</style>
