<template>
    <div>
      <Child :slides="carouselSlides" />
    </div>
  </template>
  
  <script>
  import Child from './Child.vue';
  import ProjectsSliderImages1 from '../../../../assets/OUR_PROJECTS_Slider_Images/slide-01.png'
  import ProjectsSliderImages2 from '../../../../assets/OUR_PROJECTS_Slider_Images/slide-02.png'
  import ProjectsSliderImages3 from '../../../../assets/OUR_PROJECTS_Slider_Images/slide-03.png'
  
  export default {
    components: {
      Child
    },
    data() {
      return {
        carouselSlides: [
          { text: 'Slide 1 text', image: ProjectsSliderImages1, alt: 'Image 1' },
          { text: 'Slide 2 text', image: ProjectsSliderImages2, alt: 'Image 2' },
          { text: 'Slide 3 text', image: ProjectsSliderImages3, alt: 'Image 3' }
        ],
      };
    }
  };
  </script>
  