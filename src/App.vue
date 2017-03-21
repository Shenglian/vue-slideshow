<template>
  <div id="app">
    <Slideshow
      :imgs="swiperSlides"
      :options="slideshowOptions">
    </Slideshow>
  </div>
</template>

<script>
import Slideshow from './vue-slideshow';

export default {
  name: 'app',
  components: {
    Slideshow,
  },
  data() {
    return {
      slideshowOptions: {},
      swiperSlides: [
        {
          url: 'https://source.unsplash.com/category/buildings/1600x900',
          href: '/',
        },
        {
          url: 'https://source.unsplash.com/category/food/1600x900',
        },
        {
          url: 'https://source.unsplash.com/category/nature/1600x900',
        },
        {
          url: 'https://source.unsplash.com/category/people/1600x900',
        },
        {
          url: 'https://source.unsplash.com/category/technology/1600x900',
        },
      ],
    };
  },
};
</script>
