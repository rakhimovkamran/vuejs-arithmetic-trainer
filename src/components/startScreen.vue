<!-- Template -->
<template>

    <div class="start-body">
        <h1> Are you ready ? </h1>

        <button class="start-btn btn-yes" @click='$emit("onStart")' >Yes</button>
    
    </div>

</template>
<!-- Scripts -->
<script>


// Exports
export default{ 

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
    background: rgb(7, 122, 74);
}

.btn-no:hover {
    background: rgb(133, 52, 52);
}

@keyframes blink {
    from {
        opacity: 0;
        transform: scale(1);
    }

    to {
        transform: scale(.9);
        opacity: 1;
    }
}

</style>