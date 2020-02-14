<!-- Template -->
<template>
        <div class="start-body">
                <h1> {{ x }} {{ this.operation }} {{ y }} = ? </h1>
                <div class="btn-list">
                        <button class="btn-answer" v-for='answer in answers' @click='onAnswer(answer)'> {{ answer }} </button>
                </div>
            </div>

</template>
<!-- Scripts -->
<script>

// Exports
export default{ 

    props: ['level', 'levels'],

    // Application Data
    data () {
        return {
            x : randInt(this.levels[this.level].range[0], this.levels[this.level].range[1]), // X Variable
            y : randInt(this.levels[this.level].range[0], this.levels[this.level].range[1]), // Y Variable

            // Main Operations
            operation: '',
        }
    },

    // Computed Properties
    computed: {

        operations () {
            return this.levels[this.level].operations;
        },

        rightAnswer () {
            this.operation = this.operations[ randInt(0, this.operations.length) ];

            switch (this.operation) {
                case '+': { // if operation equal +
                    return this.x + this.y;
                }

                case '-': { // if operation equal -
                    return this.x - this.y;
                }

                case '*': { // if operation equal *
                    return this.x * this.y;
                }

                // case '/': { // if operation equal *
                //     return this.x / this.y;
                // }

                default: {
                    this.operation = '+';
                    return this.x + this.y;
                }
            }
 

        },

        answers() { // Right Answer
            let answersArray = [ this.rightAnswer ];

            // Loop for add some wrong answers
            while ( answersArray.length < this.levels[this.level].variants ) {
                let wrongAnswer = randInt( this.rightAnswer - 5, this.rightAnswer + 5 );
                
                if ( answersArray.indexOf( wrongAnswer ) === -1 ) {
                    answersArray.push( wrongAnswer );
                }
            }

            /// Returning Answers Array
            return shuffle(answersArray);
        }
    },

    // Methods
    methods: {
        onAnswer ( answer ) {
            // Condition
            if ( answer === this.rightAnswer ) { // We'll emit 'Right'
                this.$emit('onRightAnswer');
            } else { // We'll emit 'Wrong'
                this.$emit('onWrongAnswer', ` ${ this.x } ${ this.operation } ${ this.y } = ${ this.rightAnswer } !`);
            }
        },
    },

}

// Modules
function randInt( min, max ) {
    // Return Random Number (min, max)
    return Math.round( Math.random() * ( max - min ) + min );
}

function shuffle ( array ) {
    let currentIndex = array.length, temporaryValue, randomIndex;

    while ( 0 !== currentIndex) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        temporaryValue = array[ currentIndex ];
        array[ currentIndex ] = array[ randomIndex ];
        array[ randomIndex ] = temporaryValue;
    }

    return array;
}

</script>
<!-- Style -->
<style scoped>

.start-body {
    width: 100%;
    height: 100%;
    text-align: center;
}

.start-body > h1 {
    text-transform: uppercase;
    font-size: 3em;
    letter-spacing: 10px;
    font-weight: lighter;
    margin-top: 120px;

    animation: blink 2s alternate-reverse infinite;
}

@keyframes blink {
    from {
        transform: scale(1);
    }

    to {
        transform: scale(.9);
    }
}

.btn-list {
    margin: 100px;
}

.btn-answer {
    width: 120px;
    height: 60px;
    transition: all .4s;
    background: transparent;
    border: 1px solid #fff;
    color: #fff;
    font-weight: lighter;
    margin: 10px;

    cursor: pointer;
}

.btn-answer:hover {
    border-color: transparent;
    transform: scale(.9);
    background: rgb(28, 121, 82);
}

</style>