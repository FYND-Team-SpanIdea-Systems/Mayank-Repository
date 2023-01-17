<template>
<div>
    <div class="loadin-page">
        <div class="loader">
            <ul class="progress">
                <li>
                    <svg viewBox="-10 -10 220 220">
                        <g fill="none" stroke-width="6" transform="translate(100,100)">
                            <path d="M 0,-100 A 100,100 0 0,1 86.6,-50" stroke="#F7E7CF" />
                            <path d="M 86.6,-50 A 100,100 0 0,1 86.6,50" stroke="#F7E7CF" />
                            <path d="M 86.6,50 A 100,100 0 0,1 0,100" stroke="#F7E7CF" />
                            <path d="M 0,100 A 100,100 0 0,1 -86.6,50" stroke="#F7E7CF" />
                            <path d="M -86.6,50 A 100,100 0 0,1 -86.6,-50" stroke="#F7E7CF" />
                            <path d="M -86.6,-50 A 100,100 0 0,1 0,-100" stroke="#F7E7CF" />
                        </g>
                    </svg>
                    <svg viewBox="-10 -10 220 220">
                        <path
                            d="M200,100 C200,44.771525 155.228475,0 100,0 C44.771525,0 0,44.771525 0,100 C0,155.228475 44.771525,200 100,200 C155.228475,200 200,155.228475 200,100 Z"
                            stroke-dashoffset="630"></path>
                    </svg>
                </li>
            </ul>
            <div class="numb">0%</div>
        </div>
    </div>
    <div class="mayank">
        <AnimationPLP />
    </div>
</div>
</template>

<script>
import AnimationPLP from './AnimationPLP.vue';

export default {
    name: "PageLoader",
    mounted() {
        this.onload();
    },
    methods: {
        onload: function () {
            let numb = document.querySelector(".numb");
            let loader = document.querySelector(".loadin-page");
            let mayank = document.querySelector(".mayank");
            mayank.style.visibility = "hidden";
            let counter = 0;
            setInterval(() => {
                if (counter >= 101) {
                    clearInterval();
                    loader.style.display = "none";
                    mayank.style.visibility = "visible";
                    // loader.style.opacity = "0";
                    // show.style.visibility = "visible";
                }
                else {
                    counter += 1;
                    numb.textContent = counter + "%";
                }
            }, 20);
        }
    },
    components: { AnimationPLP }
}
</script>

<style scoped>
.loadin-page {
    position: absolute;
    /* background-color: #f7e7cf; */
    width: 99vmax;
    /* height: 50vmax; */
    margin: 0px;
    padding: 0px;
}

.loader {
    text-align: center;
    margin-top: 17rem;
}

.progress {
    background-color: transparent;
    height: 160px;
    position: relative;
    display: inline-block;
    padding: 0;
    text-align: center;
}

ul .progress > li {
    display: inline-block;
    position: relative;
    text-align: center;
    /* color: #93a2ac; */
    font-family: Lato;
    font-weight: 100;
    margin: 2rem;
}

ul .progress > li:before {
    content: attr(data-name);
    position: absolute;
    width: 100%;
    bottom: -2rem;
    font-weight: 400;
}

.progress > li:after {
    content: attr(data-percent);
    position: absolute;
    width: 100%;
    top: 3.7rem;
    left: 0;
    font-size: 2rem;
    text-align: center;
}

.progress svg {
    width: 10rem;
    height: 10rem;
}

.progress svg:nth-child(2) {
    position: absolute;
    left: 0;
    top: 0;
    transform: rotate(-90deg);
}

.progress svg:nth-child(2) path {
    fill: none;
    stroke-width: 6;
    stroke-dasharray: 629;
    stroke: black;
    animation: load 2s reverse forwards;
}
@keyframes load {
    0% {
        stroke-dashoffset: 0;
    }
}

.numb {
    position: relative;
    top: -125px;
    font-style: oblique;
    font-size: 2rem;
}
</style>