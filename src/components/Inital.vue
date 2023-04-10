<template>
  <div class="initial container">
    <input type="text" placeholder="Your name" v-model="name" />

    <button v-if="name.length > 2" @click.prevent="handleNext">Next</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },
  methods: {
    handleNext() {
      this.$emit("goTo", 1);

      this.$emit("name", this.name);
    },
  },
};
</script>

<style lang="scss">
.initial {
  width: 100%;
}
.container {
  width: 60%;
  height: 300px;
  background: url("../assets/Curiosity blue.jpg");
  margin: 2rem 1rem;
  border-radius: 15px;
  padding: 2rem 1rem 1rem 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  input {
    background: transparent;
    color: #cdcdcd;
    border: none;
    border-bottom: 2px solid #cdcdcd;
    margin-bottom: 1rem;
    width: 300px;
    padding: 15px auto;
    letter-spacing: 1px;

    &:focus {
      border: none;
      outline: none;
      border-bottom: 2px solid #cdcdcd;
    }
  }

  button {
    width: 300px;
    padding: 0.5rem;
    border-radius: 5px;
    border: none;
    background: #2c4155;
    color: #cdcdcd;
    letter-spacing: 1px;

    &:hover {
      background: #3392d1;
      font-weight: bold;
    }
  }
}
</style>
