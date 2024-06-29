<template>
  <div>
    <Carousel
    class="bg-black"
      :slides="slidesData"
      progressBars=" flex w-full md:w-5/12 float-right  top-16 right-4 md:right-20 relative items-center gap-4 z-10"
      variant="variant1"
      test="flex flex-col md:flex-row  min-w-full"
      imageText="text-white text-lg md:text-4xl uppercase bg-black items-center  p-2 md:p-4"
      imageClass="w-full h-auto"
      nextButtonClass="bg-red-500 bg-opacity-50 text-white p-1 w-5 cursor-pointer"
      prevButtonClass="bg-red-500 bg-opacity-50 text-white p-1 w-5 cursor-pointer"
      progressBarsClass="3"
      h1Class="uppercase font-extralight text-2xl md:text-3xl xl:text-5xl mb-6 md:mb-10 xl:mb-16 leading-8"
      pClass="font-light tracking-wide text-lg md:text-xl xl:text-3xl mb-6 md:mb-10 xl:mb-16 leading-8"
      ptwoClass="font-light tracking-wide text-lg md:text-xl xl:text-3xl mb-6 md:mb-10 xl:mb-16 leading-8"
      textContainerClass="text-left w-full md:w-1/2 p-6 text-white order-2 md:order-1"
      imageContainerClass="w-full md:w-1/2 p-6 order-1 md:order-2"
      buttonsClass="buttons justify-between flex relative items-center bottom-16"
      slideNumberClass="slide-number text-red-500 text-lg md:text-2xl"
    />
  </div>
</template>

<script>
import Carousel from '../shared/components/Carousel/Carousel.vue'
import ProjectsSliderImages1 from '../../assets/OUR_PROJECTS_Slider_Images/slide-01.png'
import ProjectsSliderImages2 from '../../assets/OUR_PROJECTS_Slider_Images/slide-02.png'
import ProjectsSliderImages3 from '../../assets/OUR_PROJECTS_Slider_Images/slide-03.png'

export default {
  components: {
    Carousel
  },
  data() {
    return {
      slidesData: [{
        h1: "City Mall is a shopping <br />  destination that brings people together from all walks of life.",
        p: `To help visitors find precisely what they are <br /> looking for, we doubled down on multiple arrows <br /> in the original symbol, updated and expanded <br /> them into a navigation-friendly design system.`,
        p2: "Typography also got a bold upgrade integrating <br /> a custom Georgian adaptation of Pangram <br /> typeface.",
        image: ProjectsSliderImages1,
        alt: "Image 1",
        imageText: "City Mall"
      },

      {
        h1: 'Out of nothing, a new source of wealth - Neyco shines through. ',
        p: "Whether it’s trading cryptocurrencies or pawning your bitcoin wallets to get fast access to cash.",
        p2: "Inspired by the eternal Creation of Adam our photo series for Neyco website tries to reframe the struggle between old and new forces, and help the viewers reimagine brand new source of wealth.",
        image: ProjectsSliderImages2,
        alt: 'Image 2',
        imageText: 'Neyco'
      },
      {
        h1: 'Out of nothing, if you get tired chewing on your daily fruits and veggies, you can now drink them.',
        p2: "«Kind and Noble» or [ke-ti-li da pa-ti-o-sa-ni] in <br /> our native Georgian language isn't just a name! <br /> This noble beverage is made exclusively by <br /> mixing fresh fruit and vegetable purees to bring <br /> mother nature's kindness to humans in the <br /> most convenient form.",
        image: ProjectsSliderImages3,
        alt: 'Image 3',
        imageText: 'Kind & Noble'
      }
      ]
    };
  }
};
</script>
