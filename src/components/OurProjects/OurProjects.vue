<template>
  <div>
    <Carousel ref="carousel" class="bg-black" :slides="slidesData"
      progressBars="flex max-sm:right-14 max-md:right-24 md:right-9  lg:right-10 gap-4  h-auto max-md:w-8/12 md:w-5/12  absolute top-32 items-center  z-10"
      variant="variant1" dflex="flex flex-col md:flex-row  min-w-full  h-full" progressBarsClass="3">
      <template v-slot:slide-content="{ slide, index, currentIndex }">
        <div class="relative w-full p-6  h-auto md:w-1/2 order-1 md:order-2">
          <img :src="slide.image" :alt="slide.alt" class="w-full h-full image-mob " />
          <div
            class="text-white  text-lg md:text-4xl uppercase bg-black w-fit relative float-right  items-center bottom-24 p-10">
            <h1>{{ slide.imageText }}</h1>
            <h1>{{ slide.imageText2 }}</h1>
          </div>
          <div
            class="flex absolute justify-between left-6 right-60 bottom-32    md:bottom-6  md:left-6 md:right-80  p-4">
            <div class="slide-number text-red-500 text-lg md:text-2xl">
              0{{ currentIndex + 1 }}
            </div>
            <div class="gap-4 flex">
              <button class="bg-red-500 bg-opacity-50 text-white p-1 w-5 cursor-pointer" @click="prevSlide">
                &#10094;
              </button>
              <button class="bg-red-500 bg-opacity-50 text-white p-1 w-5 cursor-pointer" @click="nextSlide">
                &#10095;
              </button>
            </div>
          </div>
        </div>
        <div class="text-left  max-sm:bottom-10 relative p-6  text-white order-2 md:order-1 w-full md:w-1/2">
          <div class="h-full text-left">
            <h1 v-html="slide.h1"
              class="uppercase font-extralight text-2xl md:text-3xl xl:text-5xl mb-6 md:mb-10 xl:mb-72"></h1>
            <p v-html="slide.p"
              class="font-light tracking-wide text-lg md:text-xl xl:text-3xl mb-6  xl:mb-48 leading-8 "></p>
            <p v-html="slide.p2"
              class="font-light tracking-wide text-lg md:text-xl xl:text-3xl mb-6 md:mb-10 xl:mb-16 leading-8"></p>
          </div>
        </div>
      </template>
    </Carousel>
  </div>
</template>

<script>
import Carousel from '../shared/components/Carousel/Carousel.vue';
import ProjectsSliderImages1 from '../../assets/OUR_PROJECTS_Slider_Images/slide-01.png'
import ProjectsSliderImages2 from '../../assets/OUR_PROJECTS_Slider_Images/slide-02.png'
import ProjectsSliderImages3 from '../../assets/OUR_PROJECTS_Slider_Images/slide-03.png'

export default {
  components: {
    Carousel
  },
  data() {
    return {
      slidesData: [
        {
          h1: "City Mall is a shopping <br />  destination that brings people together from all walks of life.",
          p: `To help visitors find precisely what they are <br /> looking for, we doubled down on multiple arrows <br /> in the original symbol, updated and expanded <br /> them into a navigation-friendly design system.`,
          p2: "Typography also got a bold upgrade integrating <br /> a custom Georgian adaptation of Pangram <br /> typeface.",
          image: ProjectsSliderImages1,
          alt: "Image 1",
          imageText: "City Mall"
        },
        {
          h1: 'Out of nothing, a new source of wealth - Neyco shines through.',
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
  },
  methods: {
    prevSlide() {
      this.$refs.carousel.prevSlide();
    },
    nextSlide() {
      this.$refs.carousel.nextSlide();
    }
  }
};
</script>

<style scoped>
@media only screen and (max-width:768px) {
  .image-mob {
    height: 500px;
  }
}
</style>