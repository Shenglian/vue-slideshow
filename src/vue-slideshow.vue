<template>
    <div class="slideshow" 
      @mouseover="pauseSlideshow"
      @mouseleave="playSlideshow" 
    >
        <div id="slides">
            <a v-for="(source, index) in sources"
              class="slide" 
              :class="{ 'active': currentSlide(index) }" 
              :href="source.href">Slide {{ index }}
              <video 
                name="media" controls>
                <source :src="source.src" :type="source.type">
              </video>
            </a>
        </div>

        <div class="paginations">
          <div v-for="(p, index) in paginations" 
            class="pagination"
            :class="{ 'active': currentSlide(index) }"
            @click="goToSlide(index)"></div>
        </div>
        
        <div class="prev" @click="previousSlideshow"> < </div>
        <div class="next" @click="nextSlideshow"> > </div>
          
    </div>
</template>

<script>
  export default {
    name: 'slideshow',
    props: {
      names: '',
      sources: {
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
      this.paginations = this.sources.length;
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

<style lang="scss" scoped>

$slidesZIndex: 2;
$paginationsZIndex: 3;
$arrowsZIndex: 4;

// if javascript is available，
// it will replace none to block;
.slideshow {
  display: none;
  position: relative;
  height: auto;

  * {
    box-sizing: border-box;
  }
}

#slides {
    position: relative;
    height: 300px;
    padding: 0px;
    margin: 0px;
    list-style-type: none;
}

.slide {
    opacity: 0;
    position: absolute;
    left: 0;
    top: 0;
    padding: 40px;
    width: 100%;
    height: 100%;

    background-color: #333;
    background-size: cover;

    transition: opacity 1s ease-out;

    cursor: pointer;

    z-index: $slidesZIndex;
    &.active {
        opacity: 1;
    }
}

.slide {
    color: #fff;
    font-size: 40px;
}

.prev,
.next {
  position: absolute;
  top: 50%;

  font-size: 36px;
  color: #d3d3d3;

  transform: translateY(-50%);
  z-index: $arrowsZIndex;

  cursor: pointer;
}

.prev { left: 30px; }
.next { right: 30px; }

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

</style>
