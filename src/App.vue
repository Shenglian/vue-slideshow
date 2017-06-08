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
          href: '/1',
          name: 'EMI演唱會活動宣傳_20s',
          word: '904,097',
          client: '環球唱片',
          category: '影劇媒體類',
        },
        {
          url: 'https://source.unsplash.com/category/food/1200x400',
          href: '/2',
          name: 'EMI演唱會活動宣傳_20s',
          word: '904,097',
          client: '環球唱片',
          category: '影劇媒體類',
        },
        {
          url: 'https://source.unsplash.com/category/nature/1200x400',
          href: '/3',
          name: 'EMI演唱會活動宣傳_20s',
          word: '904,097',
          client: '環球唱片',
          category: '影劇媒體類',
        },
        {
          url: 'https://source.unsplash.com/category/people/1200x400',
          href: '/4',
          name: 'EMI演唱會活動宣傳_20s',
          word: '904,097',
          client: '環球唱片',
          category: '影劇媒體類',
        },
        {
          url: 'https://source.unsplash.com/category/technology/1200x400',
          href: '/5',
          name: 'EMI演唱會活動宣傳_20s',
          word: '904,097',
          client: '環球唱片',
          category: '影劇媒體類',
        },
      ],
    };
  },
};
</script>
