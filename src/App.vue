<template>
  <div id="app">
    <Slideshow
      :imgs="imgs">
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
      imgs: [
        {
          url: 'https://source.unsplash.com/category/buildings/1200x400',
          href: '/',
        },
        {
          url: 'https://source.unsplash.com/category/food/1200x400',
        },
        {
          url: 'https://source.unsplash.com/category/nature/1200x400',
        },
        {
          url: 'https://source.unsplash.com/category/people/1200x400',
        },
        {
          url: 'https://source.unsplash.com/category/technology/1200x400',
        },
      ],
    };
  },
};
</script>
