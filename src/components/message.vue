<!-- Template -->
<template>
    <div class="start-body">
        <h1 :class='type'> {{ text }} </h1>

        <div class="btn-list">
                <button 
                    class="start-btn btn-yes" 
                    :class='"btn-" + type'
                    @click='$emit("onNext")'
                >Continue</button>
        </div>

    </div>
</template>
<!-- Scripts -->
<script>

// Exports
export default{ 
    props:['type', 'text']
}

</script>
<!-- Style -->
<style scoped>

start-body {
    width: 100%;
    height: 100%;
    text-align: center;
}

.start-body > h1 {
    text-transform: uppercase;
    font-size: 3em;
    letter-spacing: 10px;
    margin-top: 120px;
    text-align: center;
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

.Wrong {
    color: rgb(133, 52, 52);
    font-weight: bolder;
}

.Right {
    color: rgb(28, 121, 82);
    font-weight: bolder;
}

.NotAnswered {
    color: rgb(232, 235, 69);
    font-family: Helvetica Neue;
    font-weight: lighter;
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

.btn-Right:hover {
    background: rgb(28, 121, 82);
}

.btn-Wrong:hover {
    background: rgb(133, 52, 52);
}

.btn-NotAnswered:hover {
    background: rgb(232, 235, 69);
    color: #000;
}

.btn-list {
    text-align: center;
}

</style>