<template>
  <transition appear @enter="enter">
    <div class="end container">
      <h1>Congratulations, {{ name }}!</h1>

      <div class="inner">
        <h3>
          You won <span> ${{ score }} </span>
        </h3>
      </div>
    </div>
  </transition>
</template>

<script>
import gsap from "gsap";
export default {
  props: ["score", "name"],
  methods: {
    enter(el, done) {
      gsap.from(el, {
        duration: 1,
        y: 200,
        onComplete: done,
      });
    },
  },
};
</script>

<style lang="scss">
.end {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  h3 {
    font-size: 1.2rem;
    color: goldenrod;
    font-family: Cinzel Decorative;
    font-weight: 400;

    span {
      font-size: 3rem;
      letter-spacing: 5px;
    }
  }
}
</style>
