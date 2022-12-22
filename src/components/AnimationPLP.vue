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

li img {
  transition: 0.25s ease-in-out;
  backface-visibility: hidden;
}

.mxx:hover img {
  transform: scale(1.2);
  transform-origin: center;
}

li:before {
  content: "";
  width: 0%;
  height: 5px;
  background: gold;
  position: absolute;
  bottom: -19px;
  /* margin-left: 0px; */
  transition: 200ms;
  z-index: 2;
}

li:nth-child(1) {
  opacity: 1;
}

li:hover {
  opacity: 1;
}

li:hover:before {
  width: 890px;
  text-align: center;
  /* margin-left: 0px; */
}
</style>