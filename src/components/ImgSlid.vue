<template>
  <div class="plp">
    <AnimationPLP />
  </div>
  
  <div class="outer-wrapper">
    <div class="inner-wrapper fadeInUp">
      <div class="front-image-wrapper">
        <img id="image-front" />
      </div>
      <div class="back-image-wrapper">
        <div id="left-btn" class="indicator-btn">
          <span>Left</span>
        </div>
        <img id="image-left" />
        <img id="image-right" />
        <div id="right-btn" class="indicator-btn">
          <span>Right</span>
        </div>
      </div>
    </div>
  </div>
  <div>
    <PageLoader />
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
    document.getElementById("image-left").src = this.imgArr[this.leftIndex];
    document.getElementById("image-front").src = this.imgArr[this.frontIndex];
    document.getElementById("image-right").src = this.imgArr[this.rightIndex];


    document.getElementById("left-btn").addEventListener("click", this.slideLeft);
    document.getElementById("right-btn").addEventListener("click", this.slideRight);
  },
  methods: {
    slideLeft: function () {
      
      let element = document.getElementById('image-front');


      setTimeout(() => {
        element.classList.add('image-leftR');
        console.log("ghjhhhhssssssssssssssssssssssssssssss",element);
        console.log("ghjhhhhssssssssssssssssssssssssssssss", element.style);

        if (this.frontIndex === 0) {
          this.frontIndex = this.n;
        } else {
          //else subtract 1 to index to 'rotate carousel'
          this.frontIndex -= 1;
        }

        this.rotateImage();

        setTimeout(() => {
          element.classList.remove("image-leftR");
        }, 1000);
      }, 500);
    },
    slideRight: function () {

      let element = document.getElementById("image-front");


      setTimeout(() => {
        element.classList.add('image-rightR');
        if (this.frontIndex === this.n) {
          this.frontIndex = 0;
        } else {
          this.frontIndex += 1;
        }

        this.rotateImage();

        setTimeout(() => {
          element.classList.remove('image-rightR');
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
      document.getElementById("image-left").src = this.imgArr[this.leftIndex];
      document.getElementById("image-front").src = this.imgArr[this.frontIndex];
      document.getElementById("image-right").src = this.imgArr[this.rightIndex];
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
  animation: fadeInUp 0.4s linear forwards;
}



.outer-wrapper {
  display: flex;
  justify-content: center;
}

.inner-wrapper {
  height: 661px;
  padding-top: 200px;
}

.front-image-wrapper {
  margin-left: 50px;
  position: absolute;
}

#image-front {
  width: 375px;
  height: 500px;
  display: block;
  z-index: 3;
}

/* .image-front_lR{
  animation: front_lR 1s linear forwards;
}

@keyframes front_lR{
  from{
    transform: rotate(0deg);
  }
  to{
    transform-origin: bottom left;
    transform: rotate(-4.09deg);
    z-index: -1;
    width: 322px;
    height: 429px;
  }
}

.image-front_rR {
  animation: front_rR 1s linear forwards;
}

@keyframes front_rR {
  from {
    transform: rotate(0deg);
  }

  to {
    transform-origin: bottom right;
    transform: rotate(4.09deg);
    z-index: -1;
    width: 322px;
    height: 429px;
  }
} */

#image-left {
  width: 322px;
  height: 429px;
  margin-left: 78px;
  animation: left 0.5s linear 0.9s forwards;
}

@keyframes left {
  to {
    transform-origin: bottom left;
    transform: rotate(-4.09deg);
    z-index: -1;
  }

}

.image-leftR {
  animation: left_R 0.5s linear forwards;
}

@keyframes left_R {
  from {
    transform-origin: bottom left;
    transform: rotate(-4.09deg);
    z-index: -2;
  }

  to {
    z-index: 0;
    transform: rotate(0deg);
    width: 375px;
    height: 500px;
  }

}

#image-right {
  width: 322px;
  height: 429px;
  left: 175px;
  position: absolute;
  animation: right 0.5s linear 0.9s forwards;
}

@keyframes right {
  to {
    transform-origin: bottom right;
    transform: rotate(4.09deg);
  }
}

.image-rightR {
  animation: rR 0.5s linear forwards;
}

@keyframes rR {
  from {
    transform-origin: bottom right;
    transform: rotate(4.09deg);
    z-index: -99;
    
  }

  to {
    z-index: 0;
    transform: rotate(0deg);
    width: 375px;
    height: 500px;
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

#right-btn {
  margin-left: 130px;
}

.indicator-btn span {
  color: #F3CFDD;
  font-weight: bold;
}

.filled {
  background-color: #FFF;
}
</style>