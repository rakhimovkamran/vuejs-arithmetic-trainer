<!-- Template -->
<template>
    <div class="start-body">
        <div class="result-h1-box">

            <h1>Developer: Rakhimov Kamran</h1>
            <h1>Designer: Rakhimov Kamran</h1> <br> <hr class="headline-hr">
            <h1>Designer # 2: Jumaev Dior</h1>

            <button class="start-btn btn-yes" @click='$emit("social", "github")'>GitHub</button>
            <button class="start-btn btn-yes" @click='$emit("social", "instagram")'>Instagram</button>
            <button class="start-btn btn-yes" @click='$emit("social", "telegram")'>Telegram</button>

        </div>
    </div>
</template>
<!-- Scripts -->
<script>

// Exports
export default{ 

    computed: {

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