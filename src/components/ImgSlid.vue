<template>
  <div>
    <PageLoader />
  </div>
  <div>
  <AnimationPLP />
  </div>
 
  
  <div class="outer-wrapper">
    <div class="inner-wrapper fadeInUp">
      <div class="hide">
        <img id="image-front" :src="imgArr[frontIndex]" />
        <img id="image-left" :src="imgArr[leftIndex]" />
        <img id="image-right" :src="imgArr[rightIndex]" />
      </div>
      <div class="back-image-wrapper">
        <div id="left-btn" class="indicator-btn">
          <span>Left</span>
        </div>
        <div id="right-btn" class="indicator-btn">
          <span>Right</span>
        </div>
      </div>
    </div>
  </div>
  

</template>

<script>
import AnimationPLP from './AnimationPLP.vue'
import PageLoader from './PageLoader.vue'
export default {
  name: "ImgSlide",
  components:{
    AnimationPLP,
    PageLoader
},
  data() {
    return {
      imgArr: [
        "https://img.freepik.com/free-photo/empty-save-texture-room-light_1258-175.jpg?w=1380&t=st=1671010336~exp=1671010936~hmac=61891c73c73803c70d8e2314ae06eb4236b7ad0cbebddc9f60441525cfc6c8a5",
        "https://img.freepik.com/free-photo/blue-concrete-textured-wall_53876-94019.jpg?w=1380&t=st=1671010376~exp=1671010976~hmac=7f24736eef8bc6bd169400d47eef9dd6d18dec2746a3c7e40b8faab18b270114",
        "https://img.freepik.com/premium-vector/dark-pine-geen-smooth-gradient-abstract-background_8087-4672.jpg?w=1380",
        "https://img.freepik.com/free-photo/abstract-textured-backgound_1258-30499.jpg?w=826&t=st=1671010424~exp=1671011024~hmac=58434ae39de8d0c9d9051e3f7331642bbabbedbb2dcc908b6435eb2c86bd2392",
      ],
      n: 0,
      leftIndex: 0,
      frontIndex: 0,
      rightIndex: 0,
    };
  },
  mounted() {
    this.n = this.imgArr.length - 1;
    this.leftIndex = this.n;
    this.frontIndex = 0;
    this.rightIndex = this.frontIndex + 1;
    document.getElementById("image-left").div = this.imgArr[this.leftIndex];
    document.getElementById("image-front").div = this.imgArr[this.frontIndex];
    document.getElementById("image-right").div = this.imgArr[this.rightIndex];


    document.getElementById("left-btn").addEventListener("click", this.slideLeft);
    document.getElementById("right-btn").addEventListener("click", this.slideRight);
  },
  methods: {
    slideLeft: function () {
      
      let Front = document.getElementById('image-front');
      let Right = document.getElementById('image-right');
      let Left = document.getElementById('image-left');
      setTimeout(() => {
        Front.classList.add('image-leftR');
        Left.classList.add('image-lefth');
        Right.classList.add('image-rightr');
        
        if (this.frontIndex === 0) {
          this.frontIndex = this.n;
        } else {
          //else subtract 1 to index to 'rotate carousel'
          this.frontIndex -= 1;
        }

        this.rotateImage();

        setTimeout(() => {
          Front.classList.remove("image-leftR");
          Right.classList.remove('image-rightr');
          Left.classList.remove('image-lefth');
        }, 1000);
      }, 500);
    },
    slideRight: function () {

      let Front = document.getElementById("image-front");
      let Left = document.getElementById('image-left');
      let Right = document.getElementById('image-right');
      setTimeout(() => {
        Front.classList.add('image-rightR');
        Left.classList.add('image-Leftr');
        Right.classList.add('image-righth');

        if (this.frontIndex === this.n) {
          this.frontIndex = 0;
        } else {
          this.frontIndex += 1;
        }

        this.rotateImage();

        setTimeout(() => {
          Front.classList.remove('image-rightR');
          Left.classList.remove('image-Leftr');
          Right.classList.remove('image-righth');
        }, 1000);
      }, 500);
    },
    rotateImage: function () {
      if (this.frontIndex == 0) {
        this.leftIndex = this.n;
        this.rightIndex = 1;

      } else if (this.frontIndex == this.n) {
        this.leftIndex = this.n - 1;
        this.rightIndex = 0;
      } else {
        this.leftIndex = this.frontIndex - 1;
        this.rightIndex = this.frontIndex + 1;
      }
      document.getElementById("image-left").div = this.imgArr[this.leftIndex];
      document.getElementById("image-front").div = this.imgArr[this.frontIndex];
      document.getElementById("image-right").div = this.imgArr[this.rightIndex];
    },
  },
};
</script>

<style scoped>
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translate3d(0, 25%, 0);
  }

  to {
    opacity: 1;
    transform: none;
  }
}

.fadeInUp {
  height: 500px;
  animation: fadeInUp 0.4s linear forwards;
}



.outer-wrapper {
  padding-left: 500px;
  padding-top: 200px;
  /* background-color: antiquewhite; */
  height: 1000px;

}


#image-front {
  width: 375px;
  height: 430px;
  position: absolute;
  /* top: -5px; */
}

#image-left {
  width: 322px;
  height: 390px;
  position: absolute;
  left: 0px;
  top:20px;
  z-index: -2;
  animation: left 0.9s 0.3s forwards ;
}

@keyframes left {
  to {
    left: -12px;
    transform-origin: bottom left;
    transform: rotate(-4.09deg);
  }

}

.image-Leftr{
  animation: LeftRRR 0.1s !important;
}
@keyframes LeftRRR {
  to{
    transform: rotate(0deg);
  }
}

.image-leftR {
  animation: left_R 0.9s linear forwards;
}

@keyframes left_R {
  from {
    width: 322px;
    height: 390px;
    left: -12px;
    transform-origin: bottom left;
    transform: rotate(-4.09deg);
    z-index: -1;
  }

  to {
    z-index: 0;
    transform: rotate(0deg);
    width: 375px;
    height: 430px;
  }

}

.image-lefth {
  opacity: -1;
  animation: 0.1s linear forwards !important;
}


#image-right {
  width: 322px;
  height: 390px;
  left: 52px;
  top: 20px;
  position: absolute;
  animation: right 0.9s 0.2s linear forwards;
  z-index: -2;
}

@keyframes right {
  to {
    left: 65px;
    transform-origin: bottom right;
    transform: rotate(4.09deg);
  }
}

.image-rightr {
  animation: rightRRR linear !important;
}

@keyframes rightRRR {
  from{
    z-index: 1;
  }
  to {
    z-index: 0;
    transform: rotate(0deg);
  }
}

.image-righth{
    opacity: -1;
    animation:  0.5s linear forwards !important;
  }
  
  

.image-rightR {
  animation: rR 0.9s linear forwards;
}

@keyframes rR {
  from {
    width: 322px;
    height: 390px;
    left: 65px;
    transform-origin: bottom right;
    transform: rotate(4.09deg);
    z-index: -1;
  }

  to {
    width: 375px;
    height: 430px;
    left: 0px;
    z-index: 0;
    transform: rotate(0deg);
    
  }

}



.back-image-wrapper {
  position: absolute;
  z-index: -1;
  /* margin-top: 50px; */
  display: inline-flex;
  align-items: center;
  transform: translateX(-72px);
}

.indicator-btn {
  background-color: darkred;
  height: 45px;
  width: 45px;
  border-radius: 50%;
  line-height: 45px;
  text-align: center;
  cursor: pointer;
}

#left-btn{
  margin-left: -110px;
}

#right-btn {
  margin-left: 670px;
}

.indicator-btn span {
  color: #F3CFDD;
  font-weight: bold;
}

.filled {
  background-color: #FFF;
}
</style>