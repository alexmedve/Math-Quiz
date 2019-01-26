<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <h1 class="text-center">The Math Quiz</h1>
      </div>
    </div>
    <hr>
    <div class="row">
      <div class="col">
        <transition name="flip" mode="out-in">
          <components :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question' "></components>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import Answer from './Components/Answer.vue'
import Question from './Components/Question.vue'

export default {
  data() {
    return {
      mode: 'app-question'
    }
  },
  methods: {
    answered(isCorrect) {
      if(isCorrect) {
        this.mode = 'app-answer';
      } 
      else {
        this.mode = 'app-question'
        alert('Wrong! Try again!')
      }
    }
  },
  components: {
    appAnswer: Answer,
    appQuestion: Question
  }
}
</script>

<style>
  .flip-enter-active {
    animation: flip-in 0.5s ease-out forwards;
  }

  .flip-leave-active {
    animation: flip-out 0.5s ease-out forwards;
  }

  @keyframes flip-out {
    from {
      transform: rotateY(0deg);
    } to {
      transform: rotateY(90deg);
    }
  }

  @keyframes flip-in {
    from {
      transform: rotateY(90deg);
    } to {
      transform: rotateY(0deg);
    }
  }
</style>
