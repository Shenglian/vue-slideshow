<template>
  <div id="app">
    <Slideshow
      :sources="sources"
      :names="names">
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
      names: 'sss',
      sources: [
        {
          src: 'https://media.w3.org/2010/05/sintel/trailer.mp4',
          type: 'video/mp4',
        },
        {
          src: 'https://media.w3.org/2010/05/sintel/trailer.mp4',
          type: 'video/mp4',
        },
        {
          src: 'https://media.w3.org/2010/05/sintel/trailer.mp4',
          type: 'video/mp4',
        },
        {
          src: 'https://media.w3.org/2010/05/sintel/trailer.mp4',
          type: 'video/mp4',
        },
        {
          src: 'https://media.w3.org/2010/05/sintel/trailer.mp4',
          type: 'video/mp4',
        },
      ],
    };
  },
};
</script>
