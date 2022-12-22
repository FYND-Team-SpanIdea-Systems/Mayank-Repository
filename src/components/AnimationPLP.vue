<template>
  <div id="slider">
    <div class="slide">
      <ul class="mxx">
        <li v-for="items in this.img" :key="items">
          <img :src="items" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "AnimationPLP",
  data() {
    return {
      img: [
        "http://i.hizliresim.com/WgXZpN.jpg",
        "http://i.hizliresim.com/3vOalr.jpg",
        "http://i.hizliresim.com/R1gVpa.jpg",
        "http://i.hizliresim.com/pX5oMq.jpg"

      ],
    };
  },
  mounted() {},
};
</script>

<style scoped>
#slider {
  margin: 20px;
  width: 1000px;
  height: 418px;
  overflow: hidden;
}

.slide {
  width: 100%;
  height: 400px;
  /* overflow: hidden; */
}

.slide ul {
  display: flex;
  list-style: none;
}

@keyframes slider {
  from {
    transform: translate3d(0px, 0px, 0px);
  }

  to {
    transform: translate3d(-3000px, 0px, 0px);
  }
}

#slider ul:hover {
  animation: 6s slider linear both;
}

.mxx {
  width: 100%;
  height: 100%;
}

.mxx img {
  transition: 0.25s ease-in-out;
  backface-visibility: hidden;
}

.mxx:hover img {
  transform: scale(1.2);
  transform-origin: center;
}

div:before {
  content: "";
  width: 0%;
  height: 5px;
  background: black;
  position: absolute;
  top: 432px;
  margin-left: 0px;
  transition: 200ms;
  z-index: 2;
}

div:nth-child(n) {
  opacity: 1;
}

div:hover {
  opacity: 1;
}

div:hover:before {
  width: 1000px;
  /* margin-left: 0%; */
}
</style>