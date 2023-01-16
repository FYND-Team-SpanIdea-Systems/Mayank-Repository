<template>
    <div class="main-container">
        
        <div class="container">
            <div class="container" v-for="(image,index) in images">
                <img v-bind:src="image" :key="index" v-if="index === currentIndex"  />
            </div>
            <div v-show="visible" class="indicator-container">
                <span v-for="(image,index) in images" v-bind:class="{ active: (image, index) === currentIndex }"
                    ></span>
            </div>
        </div>
        <div class="transparent-div" @mouseleave="imgHoverout" @mouseenter="imgHover">
            
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            images: [
                'https://i.postimg.cc/QNYkPnvr/p1.jpg',
                'https://i.postimg.cc/W1B5yfF4/p2.jpg',
                'https://i.postimg.cc/h40PPkcH/p4.jpg',
            ],
            currentIndex: 0,
            myInterval : '',
            statesCount: 1,
            visible : false
            // setIntervalid : '',
        }
    },
    methods: {
        imgHover() {
            this.myInterval =  setInterval(() => {
                this.currentIndex = (this.currentIndex + 1 + this.images.length) % this.images.length;
               },1500)
               this.visible = true;
            console.log("Inside", this.myInterval);
        },
        imgHoverout(){
            this.currentIndex = 0 ;
            this.visible = false;
            clearInterval(this.myInterval);
            console.log("Outside", this.myInterval)
        }

    },
}
</script>

<style scoped>
.main-container {
    margin: auto;
    margin-top: 250px;
    margin-bottom: 250px;
    position: relative;
}
.transparent-div{
    border: 1px solid black;
    background-color: transparent;
    width: 298px;
    height: 522px;
    position: absolute;
    left: 790px;
    top: 0px;
    opacity: 0;
}

.container {
    width: 325px;
    overflow: hidden;
}

img {
    transition: opacity 0.9s ease-in-out;
    width: 320px;
    height: 522px;
}

.indicator-container {
    display: flex;
    margin: auto;
    width: 100%;
    /* position: relative; */
    top: -3px;
    margin-left: 12px;
}

.indicator-container span {
    width: 100%;
    height: 4px;
    background-color: gray;
}

span.active {
    transition: 0.3 ease-in-out;
    width: 100%;
    height: 4px;
    background-color: black;
    opacity: 1;
}
</style>
