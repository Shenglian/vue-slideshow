<template>
    <div class="slideshow" 
      @mouseover="pauseSlideshow"
      @mouseleave="playSlideshow" 
    >
      <div id="slides">
        <a v-for="(img, index) in imgs" 
          class="slide" 
          :class="{ 'active': currentSlide(index) }" 
          :href="img.href">
            <div class="slide_content">
              <div class="slide_content__title">{{ img.name }}</div>
              <div class="slide_content__word">{{ img.word }}<span>曝光數</span></div>
              <div class="slide_content__meta"> {{ `${img.client} ${img.category}` }} </div>
            </div>
            <img :src="img.url" alt="">
          </a>
      </div>

      <div class="paginations">
        <div v-for="(p, index) in paginations" 
          class="pagination"
          :class="{ 'active': currentSlide(index) }"
          @click="goToSlide(index)"></div>
      </div>
      
      <div class="prev" @click="previousSlideshow"> 
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="15 18 9 12 15 6"/>
        </svg>
      </div>
      <div class="next" @click="nextSlideshow"> 
        <svg xmlns="http://www.w3.org/2ffffff/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#ffffff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="9 18 15 12 9 6"/>
        </svg>
      </div>
    </div>
</template>

<script>
  export default {
    name: 'slideshow',
    props: {
      imgs: {
        type: Array,
        required: true,
        default() { return []; },
      },
      seconds: {
        type: Number,
        default() { return 5000; },
      },
    },
    data() {
      return {
        currentIndex: 0,
        paginations: [],
        timer: null,
      };
    },
    mounted() {
      this.init();
      this.paginations = this.imgs.length;
    },
    methods: {
      currentSlide(val) {
        return val === this.currentIndex;
      },
      init() {
        this.$el.style.display = 'block';
        this.slides = this.$el.querySelectorAll('#slides .slide');
        this.timer = setInterval(this.nextSlideshow, this.seconds);
      },
      pauseSlideshow() {
        clearInterval(this.timer);
      },
      playSlideshow() {
        this.timer = setInterval(this.nextSlideshow, this.seconds);
      },
      previousSlideshow() {
        this.goToSlide(this.currentIndex - 1);
      },
      nextSlideshow() {
        this.goToSlide(this.currentIndex + 1);
      },
      goToSlide(n = 0) {
        // 1 % 5 = 1, 2 % 5 = 2, 3 % 5 = 3, 4 % 5 = 4, and 5 % 5 = 0
        this.currentIndex = (this.slides.length + n) % this.slides.length;
      },
    },
  };
</script>

<style lang="scss">

$slidesZIndex: 2;
$activeZIndex: 3;
$shadowZIndex: 4;
$paginationsZIndex: 10;
$arrowsZIndex: 11;

.slideshow {
  display: none;
  position: relative;
  height: auto;

  * { box-sizing: border-box; }
}

#slides {
  position: relative;
  height: 400px;
  padding: 0px;
  margin: 0px;
  list-style-type: none;

  &:hover img {
    transform: scale(1.05, 1.05);
  }
}

.slide {
  overflow: hidden;
  opacity: 0;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;

  background-color: #333;

  color: #fff;
  font-size: 40px;

  transition: opacity 1s ease-out;

  cursor: pointer;
  z-index: $slidesZIndex;

  &.active {
    opacity: 1;
    z-index: $activeZIndex;
  }

  &:after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 75%;
    bottom: 0;
    background: -webkit-linear-gradient(left,#000 0,#000 40%,transparent 100%);
    background: linear-gradient(to right,#000 0,#000 40%,transparent 100%);
  }
  &:before {
    content: '';
    position: absolute;
    top: 0;
    left: 35%;
    right: 0;
    bottom: 0;
    background: -webkit-linear-gradient(right,#000 0,#000 50%,transparent 100%);
    background: linear-gradient(to left,#000 0,#000 50%,transparent 100%);
    z-index: 1;
  }
}

.slide {
  display: flex;
  justify-content: center;
  align-items: center;
  .slide_content {
    position: absolute;
    top: 50%;
    left: 7rem;
    right: 7rem;
    text-align: right;
    transform: translate(0, -50%);
    z-index: 1;
    font-weight: 100;
    &__title { font-size: 32px; }
    &__word { 
      font-size: 55px; 
      span {
        margin-left: 30px;
        font-size: 18px;
      }
    }
    &__meta { font-size: 18px; }
  }

  img {
    position: relative;
    right: 12%;
    height: 100%;
    transition: all, .8s;
  }
}

.prev,
.next {
  position: absolute;
  top: 50%;
  
  display: flex;
  justify-content: center;
  align-items: center;

  width: 50px;
  height: 50px;

  transform: translateY(-50%) scale(2);
  z-index: $arrowsZIndex;
  cursor: pointer;
  svg { transition: all, .3s; }
  &:hover {
    svg { stroke: #adadad; }
  }
}

.prev { left: 3.4375rem; }
.next { right: 3.4375rem; }

.paginations {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 20px;

  display: flex;
  justify-content: center;

  z-index: $paginationsZIndex;

  .pagination {
    margin: auto 5px;
    width: 10px;
    height: 10px;
    border-radius: 100%;
    border: 1px solid #333;
    background-color: #333;

    cursor: pointer;
    transition: all, .3s;
    &:hover {
      border: 1px solid #999999;
      background-color: #999999;
    }
    &.active {
      background-color: #fff;
    }
  }
}

// @media screen and (min-width: 1401px) {
//   .slide:after { box-shadow: 8.23em 0 8.23em 20px rgba(0, 0, 0, 0.8) inset, -8.23em 0 8.23em 20px rgba(0, 0, 0, 0.8) inset; }
// }

// @media screen and (min-width: 1171px) and (max-width: 1400px) {
//   .slide:after { box-shadow: 7.23em 0 7.23em 20px rgba(0, 0, 0, 0.8) inset, -7.23em 0 7.23em 20px rgba(0, 0, 0, 0.8) inset; }
// }

// @media screen and (min-width: 931px) and (max-width: 1170px) {
//   .slide:after { box-shadow: 6.23em 0 6.23em 20px rgba(0, 0, 0, 0.8) inset; }
// }

// @media screen and (min-width: 768px) and (max-width: 930px) {
//   .slide:after { box-shadow: 5.23em 0 5.23em 20px rgba(0, 0, 0, 0.8) inset; }
// }

// @media screen and (max-width: 767px) {
//   .slide:after { box-shadow: 4.23em 0 4.23em 20px rgba(0, 0, 0, 0.8) inset; }
// }

</style>
