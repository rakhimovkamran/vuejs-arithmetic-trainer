<!-- Template -->
<template>

  <div class="container">

    <!-- Headlines -->

    <h1 class='headline' v-if='gameOver == false && state != "author"'> Arithmetic Trainer - Level {{ this.level + 1 }} </h1>
    <h1 class='headline' v-if='gameOver == true && state != "author"'> Game Over !</h1>
    <h1 class='headline' v-if='state == "author"'>Author</h1>
    <hr class="headline-hr">

    <!-- Progress Bar -->
    <div class="progress-body" :style='progressBodyStyle' id="progress">
      <div class="progress-bar" :style="progressBar"></div>
    </div>

    <!-- Timer Bar -->
    <div class="progress-body timer-body" :style='progressBodyStyle' id="timer" >
      <div class="progress-bar timer-bar" :style="timerBar"></div>
    </div>
    <!-- // Main Box for Animation -->
    <div class="box">
    <!-- // Transition -->
    <transition name='flip' mode='out-in'>
    <!-- Start Screen -->
    <app-start-screen 
      v-if=' state === "start" '
      @onStart = 'onStart'
    ></app-start-screen>

    <!-- Question Screen -->
    <app-question 
      v-else-if=' state === "question" '
      @onRightAnswer = 'onRightAnswer'
      @onWrongAnswer = 'onWrongAnswer'
      :levels = 'levels'
      :level = 'level'

    ></app-question>

    <!-- Message Screen -->
    <app-message 
      v-else-if=' state === "message" '
      :type  = 'answerMsg.type'      
      :text  = 'answerMsg.text' 
      @onNext = 'onNext'     
    ></app-message>

    <!-- Result Screen -->
    <app-result-screen 
      v-else-if=' state === "result" ' 
      :stats='answerStats'
      @repeatLevel = 'onRepeat'
      @nextLevel = 'nextLevel'
    ></app-result-screen>

    <!-- Result Screen -->
    <app-gameresult-screen 
      v-else-if=' state === "gameResult" ' 
      :gameStats = 'gameStats'
      :maxAnswers = 'gameMaxAnswers'
      :level = 'level'
      :levels = 'levels'
      @repeatLevel = 'onStartNewGame'
      @authorScreen = 'author'
    ></app-gameresult-screen>

    <app-author-screen 
    v-else-if=' state === "author" ' 
  ></app-author-screen>

    <div v-else=''> <h1>Unknown State... </h1> </div>
  </transition>
    </div>

    <!-- // When State is Unknown -->

  </div>

</template>
<!-- Scripts -->
<script>

  // Including Components
  Vue.component('app-start-screen',    require('./startScreen.vue').default);
  Vue.component('app-question',           require('./question.vue').default);
  Vue.component('app-message',             require('./message.vue').default);
  Vue.component('app-result-screen',  require('./resultScreen.vue').default);
  Vue.component('app-gameresult-screen',  require('./gameResult.vue').default);
  Vue.component('app-author-screen',  require('./author.vue').default);

  // Config
  export default {

    // Data Attribute
    data(){
      return {

        // Timer Delay
        timerValue: 0,
        timerMax: 10,

        // Application State
        state: 'start',
        gameOver: false,

        // Answer Stats
        answerStats: {
          right: 0,
          wrong: 0,
          notAnswered: 0
        },

        gameStats: {
          right: 0,
          wrong: 0,
          notAnswered:0,
          maxAnswers: 0
        },

        // Answer Messages
        answerMsg: {
          type: '',
          text: ''
        },

        // Max Questions quantity
  
        level: 0,
        levels: [
          { // 1 st Level 
            maxAnswers: 10,
            variants: 2,
            range:[1, 10],
            operations:[, '+'],

            timer: 10
          },

        ]
      }

      
    },

    // Methods
    methods: {

      /// TIMER FUNCTIONS ALL
      TimerStart() {

        this.timerValue = this.timerMax;

        this.interval = setInterval(() => {
          this.timerValue -= 1;
          if ( this.timerValue === 0 ) {
            setTimeout(() => {
              this.TimerStop();
              this.onNotAnswer();
            }, 500)
          }

        }, 1000)

      }, TimerStop() {
        this.timerValue = this.timerMax;
        clearInterval( this.interval );
      }, 

      // When we click 'YES' button
      onStart () {

        this.timerMax = this.levels[ this.level ].timer;

        this.gameOver = false;

        // Running Timer
        this.TimerStart();
              
        // Repeat Stage
        this.state = 'question';

        // Update Stats
        this.answerStats.right = 0;
        this.answerStats.wrong = 0;
        this.answerStats.notAnswered = 0;
      },


      author () {
        this.state = 'author';
      },


      onStartNewGame () {

        this.timerMax = this.levels[ this.level ].timer;

        this.gameStats.right = 0;
        this.gameStats.wrong = 0;
        this.gameStats.notAnswered = 0;
        this.gameStats.maxAnswers = 0;
        this.level = 0;

        this.gameOver = false;

        // Running Timer
        this.TimerStart();
              
        // Repeat Stage
        this.state = 'question';

        // Update Stats
        this.answerStats.right = 0;
        this.answerStats.wrong = 0;
        this.answerStats.notAnswered = 0;
      },

      onRepeat () {

        // Running Timer
        this.TimerStart();
              
        // Repeat Stage
        this.state = 'question';

        this.gameStats.right -= this.answerStats.right;
        this.gameStats.wrong -= this.answerStats.wrong;
        this.gameStats.notAnswered -= this.answerStats.notAnswered;

        // Update Stats
        this.answerStats.right = 0;
        this.answerStats.wrong = 0;
        this.answerStats.notAnswered = 0;
      },
          // Cheking Answers from 'question' state
    onRightAnswer ()    { // When answer is Right

      this.TimerStop();

        this.state = 'message'; // On 'msg' State

      // Change Answer Message
      this.answerMsg.text = 'Excellent !' // Right
      this.answerMsg.type = 'Right';

      // Change Stats
      this.answerStats.right += 1;
      this.gameStats.right += 1;
    },

    onNotAnswer () {

      this.answerMsg.text = `Time is out`;
      this.answerMsg.type = 'NotAnswered';
      this.answerStats.notAnswered += 1;
      this.state = 'message';

      this.gameStats.notAnswered += 1;

    },

    onWrongAnswer (msg) { // When answer is Wrong

      this.TimerStop();

      this.state = 'message'; // // On 'msg' State

      // Change Answer Message
      this.answerMsg.text = msg; // Wrong
      this.answerMsg.type = 'Wrong';

      // Change Stats
      this.answerStats.wrong += 1;

      this.gameStats.wrong += 1;

    },

    // Next Question
    onNext () {

      if ( this.answerDone < this.answerMax ) {
        this.state = 'question';
        this.TimerStart();
      } else if ( this.levels[ this.level + 1 ] === undefined ) {
        this.state = 'gameResult';
        this.gameOver = true;
      } else {
        this.state = 'result';
      }
    },

    // Next Level
    nextLevel () {

      if ( this.levels.length < this.level ) {
        this.level = 0;
        this.onStart();
      } else {
        this.level += 1;
        this.timerMax = this.levels[ this.level ].timer;
        this.gameStats.maxAnswers += this.levels[ this.level ].maxAnswers;
        this.onStart();

      }
    }


    },

    computed: {

      gameMaxAnswers () {
        let max = 0;
        for ( let i of this.levels ) {
          max += i.maxAnswers;
        }

        return max;
      },

      answerMax () {
        return this.levels[this.level].maxAnswers;
      },

      answerDone () {
        return this.answerStats.right + this.answerStats.wrong + this.answerStats.notAnswered;
      },

      progressBar () {
          return {
          width: (this.answerDone / this.answerMax * 100) + '%',
          background: this.progressBarColor
        } 
      },

      timerBar () {
        return {
          width: (this.timerValue / this.timerMax * 100) + '%',
          background: this.timerBarColor
        }
      },

      progressBodyStyle () {
        if ( this.gameOver === false ) {
          return true
        } else if ( this.gameOver === true ) {
          return {
            height : 0,
            opacity: 0
          }
        }
      },

      progressBarColor () {
        if ( this.answerStats.right > this.answerStats.wrong ) {
          return 'rgb(28, 121, 82)';
        } else if ( this.answerStats.right === this.answerStats.wrong ) {
          return 'rgb(232, 235, 69)';
        } else if ( this.answerStats.right < this.answerStats.wrong ) {
          return 'rgb(133, 52, 52)';
        }
      },

      timerBarColor () {
        let yellow =  'rgb(232, 235, 69)', // Yellow
            red    =  'rgb(133, 52, 52)', // Red
            green  =  'rgb(28, 121, 82)';
        
        if ( this.timerValue <= this.timerMax / 3 ) {
          return red;
        } else if ( this.timerValue < 2 * this.timerMax / 3 ) {
          return yellow;
        }
      }
    }

  }

</script>
<!-- Style -->
<style>
/* Progress Bar */
.container {
  perspective: 900px;
}
.progress-body {
  width: 100%;
  height: 40px;
  background: rgba(0,0,0,.2);
  transition: all .4s;
}

.timer-body {
  margin: 0 auto;
  height: 20px;
}


.progress-bar {
  width: 0%;
  height: 40px;
  background:  rgb(28, 121, 82);
  transition: all 2s;
}

.timer-bar {
  width: 100%;
  height: 20px;
  background: rgb(28, 121, 82);
  border-top: 5px solid rgba(0, 0, 0, .5);
  transition: all .3s;
}

  .flip-enter-active {
    animation: flipInX .3s linear;
  }

  .flip-leave-active {
    animation: flipOutX .3s linear;
  }

  /* // Animations */
  @keyframes flipInX {
    from { 
      opacity:0;
      transform: rotateX(30deg) scale(.8);
    }
    to { 
      opacity: 1;
      transform: rotateX(0deg) scale(1);
    }
  }

  @keyframes flipOutX {
    from { 
      opacity: 1; 
      transform: rotateX(0deg) scale(1);
    }
    to { 
      opacity: 0;
      transform: rotateX(30deg) scale(.8);
    }
  }
</style>