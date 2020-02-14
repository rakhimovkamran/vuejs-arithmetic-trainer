<!-- Template -->
<template>
    <div class="start-body">
        <div class="result-h1-box">

                <div class="stats-box">
                    <div class="right-stats stats-box-stat" :style="rightStats" v-if='this.gameStats.right != 0'>{{ this.rightStats.width }}</div><div class="wrong-stats stats-box-stat" :style="wrongStats" v-if='this.gameStats.wrong != 0' >{{this.wrongStats.width}}</div><div class="not-answered-stats stats-box-stat" :style="notAnswerStats" v-if='this.gameStats.notAnswered != 0'>{{this.notAnswerStats.width}}</div>
                </div>
                <!-- <h1 class="result-h1"><span style='color:rgb(28, 121, 82)'>Right</span> Answers:</h1>
                <h1 class="result-h1"><span style="color:rgb(133, 52, 52)">Wrong</span> Answers:</h1>
                <h1 class="result-h1"><span style="color:rgb(235, 223, 59)">Not Answered</span>: </h1> -->
        </div>

        <div class="result-h1-box">
                <h1 class="result-h1"><span style='color:rgb(28, 121, 82)'>Right</span> Answers: {{ this.gameStats.right }}</h1>
                <h1 class="result-h1"><span style="color:rgb(133, 52, 52)">Wrong</span> Answers: {{ this.gameStats.wrong }}</h1>
                <h1 class="result-h1"><span style="color:rgb(235, 223, 59)">Not Answered</span>: {{ this.gameStats.notAnswered }} </h1>
        </div>
        
        <button class="start-btn btn-yes" @click='$emit("repeatLevel")'>Play Again</button>
        <button class="start-btn btn-no" @click='$emit("authorScreen")'>Author</button>
    </div>
</template>
<!-- Scripts -->
<script>

// Exports
export default{ 
    props:[ 'gameStats', 'level', 'levels', 'maxAnswers' ],

    computed: {

        rightStats () {
            let rightAnswers =  this.gameStats.right;

            return {
                width: ((( rightAnswers ) * 100) / this.maxAnswers ).toFixed(0) + '%'
            }
        },

        wrongStats () {
            let wrongAnswers =  this.gameStats.wrong;

            return {
                width: ((( wrongAnswers ) * 100) / this.maxAnswers).toFixed(0) + '%'
            }
        },

        notAnswerStats () {
            let notAnswers =  this.gameStats.notAnswered;

            return {
                width: ((( notAnswers ) * 100) / this.maxAnswers).toFixed(0) + '%'
            }
        }
    }

}
    
</script>
<!-- Style -->
<style scoped>


.start-body {
    width: 100%;
    height: 100%;
    text-align: center;
}

.start-body > .result-h1-box > h1 {
    text-transform: uppercase;
    font-size: 2em;
    letter-spacing: 10px;
    font-weight: lighter;
    margin-top: 10px;

    animation: blink 2s alternate-reverse infinite;
}

.stats-box {
    width: 100%;
    height: 50px;
    background: rgba(0,0,0,.4);
    line-height: 50px;
    font-size: 1.4em;
}

.stats-box-stat {
    display: inline-block;
    transition: all 10s;
    height: 50px;
}

/* Right Answers Percent */
.right-stats {
    width: 0%;
    background: rgb(28, 121, 82);
}


/* Wrong Answers Percent */
.wrong-stats {
    width: 0%;
    background: rgb(133, 52, 52);
}

/* Right Answers Percent */
.not-answered-stats {
    width: 0%;
    background: rgb(232, 235, 69);
    color: #000;
}


.result-h1-box {
    margin-top: 40px;
}

.start-btn {
    width: 200px;
    height: 70px;
    margin: 20px;
    margin-top: 100px;
    transition: all .4s;
    background: transparent;
    color: #fff;
    border: 1px solid #fff;
    text-transform: uppercase;
    font-weight: lighter;
    cursor: pointer;
}

.start-btn:hover {
    transform: scale(.9);
    border-color: transparent;
}

.btn-yes:hover {
    background: rgb(28, 121, 82);
}

.btn-no:hover {
    background: rgb(35, 140, 201);
}

@keyframes blink {
    from {
        transform: scale(1);
    }

    to {
        transform: scale(.9);
    }
}

.result-h1 {
    margin: 0;
}
    
</style>