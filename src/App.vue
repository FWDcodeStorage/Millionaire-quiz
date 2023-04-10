<template>
  <h1>Who Wants to Be a Millionaire?</h1>
  <hr />
  <div class="app">
    <Transition appear @enter="enter">
      <component
        :is="screens[position]"
        :name="name"
        @name="handleName"
        @goTo="handleGoTo"
      />
    </Transition>
  </div>
</template>

<script>
import Inital from "./components/Inital.vue";
import Welcome from "./components/Welcome.vue";
import Game from "./components/Game.vue";
import gsap from "gsap";

export default {
  components: {
    Inital,
    Welcome,
    Game,
  },
  data() {
    return {
      screens: ["Inital", "Welcome", "Game", "End"],
      position: 0,
      name: "",
      score: "",
    };
  },

  methods: {
    enter(el, done){
      gsap.from(el, {
        duration: 1,
        y: 150,
        onComplete: done
      })
    },
    handleName(name) {
      this.name = name;
    },
    handleGoTo(position) {
      this.position = position;
    },
    // checkCorrect(questions) {
    //   if (this.isDone == true) {
    //     const green = questions.filter((q) => q.correct == true);
    //     return (this.correctAns = green);
    //   }
    // },
    // checkResult(answer) {
    //   answer.selected = true;
    //   this.isDone = true;
    //   if (answer.correct == false) {
    //     this.handleToast({ type: "error", message: "Wrong!" });
    //     this.color = "5px solid #dc3545";
    //     answer.red = true;
    //     answer.green = false;
    //     if (this.lIndex < this.levels.length) {
    //       this.lIndex = this.lIndex + 1;
    //     } else return this.lIndex;
    //     console.log("false ");
    //   } else {
    //     this.handleToast({ type: "success", message: "Correct!" });
    //     this.color = "5px solid #028202";
    //     answer.green = true;
    //     answer.red = false;
    //     this.lIndex = this.lIndex - 1;
    //     console.log("true");
    //   }
    // },
    // handleNext() {
    //   //Dovrsiti!
    //     if(this.qIndex < this.questions.length -1) {
    //       setTimeout(() => {
    //         this.qIndex = this.qIndex + 1;
    //         this.isDone = false;
    //       }, 3000);
    //       this.handleToast({
    //         type: "success",
    //         message: "Correct answer is " + this.correctAns[0].text,
    //       });
    //     } else  {
    //       console.log("end")
    //       this.$emit('goTo', 3);
    //     }

    // },
    // handleToast(values) {
    //   this.$toast.show(values.message, {
    //     type: values.type,
    //     position: "top",
    //     duration: 2000,
    //   });
    // },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Noto+Serif&display=swap");

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #cdcdcd;
  letter-spacing: 1px;
  padding: 1rem 0;
  background: url("./assets/Between Night and Day.jpg");

  h1 {
    font-size: 2rem;
    color: goldenrod;
    font-family: Cinzel Decorative;
    font-weight: 400;
  }
  .app {
    max-width: 100vw;
    max-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;

    .fade-enter-from,
    .fade-leave-to {
      opacity: 0;
    }
    .fade-enter-active,
    .fade-leave-active {
      transition: 0.5s;
    }
    .fade-enter-to,
    .fade-leave-from {
      opacity: 1;
    }
  }
}
</style>
