<template>
    <div>
        <div class="markBox">
            <div class="markerTitle">陪烧车间</div>
            <div class="marker"></div>
            <div class="markerShadow"></div>
            <div class="markerCircle"></div>
        </div>
    </div>
</template>

<script setup lang="ts">
console.log(123123);
</script>
<style>
.markBox {
    width: 100px;
    height: 80px;
    background-color: rgb(66, 132, 132);
    position: relative;
}

.markerTitle {
    position: absolute;
    font-family: "Times New Roman", serif;
    left: 50%;
    transform: translateX(-50%);
    font-size: 16px;
    font-weight: 900;
    color: rgb(194, 16, 16);
    white-space: nowrap;
    text-shadow: 
    0px 0px 1px #0a0a0a,
    0px 0px 2px #fff,
    0px 0px 3px #fff,
    0px 0px 4px #fff,
    0px 0px 5px #fff;
    /* -webkit-text-stroke:1px white; */
    /* text-stroke: 1px white; */
}

.marker {
    position: absolute;
    width: 20px;
    height: 20px;
    background-color: #F59A23;
    left: 50%;
    transform: translateX(-50%) rotate(-45deg);
    top: 30%;
    border-radius: 50%;
    border-bottom-left-radius: 0;
    z-index: 10;
}

.markerShadow {
    z-index: 8;
    position: absolute;
    width: 16px;
    height: 16px;
    background-color: #57585C;
    left: 50%;
    top: 46%;
    border-radius: 50%;
    transform: translateX(-50%);
}

@keyframes circleDong {
    0% {
        transform: scale(0.1);
        border: 1px solid #fff;
        opacity: 1;
    }
    /* 50% {
        transform: scale(1);
        border: 3px solid #fff;
        opacity: 0.3;
       
    } */
    100%{
        border: 3px solid #fff;
        transform: scale(1.5);
        opacity: 0;
    }
}

.markerCircle {
    z-index: 9;
    position: absolute;
    width: 14px;
    height: 14px;
    left: 41%;
    top: 46%;
    border-radius: 50%;
    animation-name: circleDong;
    animation-duration: 2s;
    animation-iteration-count: infinite; /* 设置动画无限循环 */
    transform-origin: center center;
}
</style>
