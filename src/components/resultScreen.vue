<!-- Template -->
<template>
    <div class="start-body">
        <div class="result-h1-box">
                <h1 class="result-h1"><span style='color:rgb(28, 121, 82)'>Right</span> Answers: {{stats.right}}</h1>
                <h1 class="result-h1"><span style="color:rgb(133, 52, 52)">Wrong</span> Answers: {{stats.wrong}}</h1>
                <h1 class="result-h1"><span style="color:rgb(235, 223, 59)">Not Answered</span>: {{stats.notAnswered}}</h1>
        </div>

        <button class="start-btn btn-yes" @click='$emit("repeatLevel")'>Repeat</button>
        <button class="start-btn btn-no" @click='$emit("nextLevel")'>Next Level</button>
    </div>
</template>
<!-- Scripts -->
<script>

// Exports
export default{ 
    props:[ 'stats' ]
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

.result-h1-box {
    margin-top: 100px;
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