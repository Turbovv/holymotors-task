<template>
  <div>
    <Carousel :slides="slidesData" class="bg-red-500" ref="carousel" variant="variant2"
      dflex="flex flex-col md:flex-row min-w-full h-full" progressBarsClass="4"
      progressBars="flex   justify-center items-center max-sm:left-12 max-lg:w-10/12 md:w-10/12 max-md:left-14 md:left-32 max-lg:gap-5  relative top-10 md:top-16  md:gap-10 z-20">
      <template v-slot:slide-content="{ slide, index, currentIndex }">
        <div class="w-full h-auto p-6  md:p-10 order-1 md:order ">
          <div class="h-full relative  ">
            <div class="absolute bottom-0 max-lg:w-5/12  border   left-0 right-0 flex justify-between items-center p-4 lg:hidden">
              <div class="slide-number text-black text-lg md:text-2xl">
                0{{ currentIndex + 1 }}
              </div>
              <div class="gap-4 flex">
                <button class="bg-black bg-opacity-50 text-white p-1 w-5 cursor-pointer" @click="prevSlide">
                  &#10094;
                </button>
                <button class="bg-black bg-opacity-50 text-white p-1 w-5 cursor-pointer" @click="nextSlide">
                  &#10095;
                </button>
              </div>
            </div>

            <img :src="slide.image" :alt="slide.alt" class="w-full h-full image-mob   object-cover" />
            <div class="   absolute bottom left-0 right-0 md:relative md:bottom-80 bg-opacity-50 text-white md:flex">
              <div class="p-6 md:p-10  w-full   relative mob   right-5 xl:absolute ">
                <p v-html="slide.p" class="font-light text-sm  xl:mb-10 tracking-wide"></p>
                <p v-html="slide.p2" class="font-light text-sm md:text-lg tracking-wide"></p>
              </div>
              <div
                class="text-white uppercase bg-red-500 md:h-fit absolute right-0 imageText-mob max-md:bottom-36 max-sm:p-2 max-md:p-10 md:top-28 items-center md:p-20">
                <h1 class="lg:text-2xl">{{ slide.imageText }}</h1>
                <h1 class="lg:text-2xl">{{ slide.imageText2 }}</h1>
              </div>
            </div>

            <div class="hidden lg:flex absolute top-10 left-20 right-20  justify-between  p-4">
              <div class="slide-number text-black font-bold text-lg md:text-2xl">
                0{{ currentIndex + 1 }}
              </div>
              <div class="gap-4 flex">
                <button class="bg-black bg-opacity-50 text-white p-1 w-5 cursor-pointer" @click="prevSlide">
                  &#10094;
                </button>
                <button class="bg-black bg-opacity-50 text-white p-1 w-5 cursor-pointer" @click="nextSlide">
                  &#10095;
                </button>
              </div>
            </div>
          </div>
        </div>
      </template>
    </Carousel>
  </div>
</template>

<script>
import Carousel from '../shared/components/Carousel/Carousel.vue';
import OurWORKSImage1 from '../../assets/OUR_WORKS_Slider_Images/slide-01.png';
import OurWORKSImage2 from '../../assets/OUR_WORKS_Slider_Images/slide-02.png';
import OurWORKSImage3 from '../../assets/OUR_WORKS_Slider_Images/slide-03.png';
import OurWORKSImage4 from '../../assets/OUR_WORKS_Slider_Images/slide-04.png';

export default {
  components: {
    Carousel
  },
  data() {
    return {
      slidesData: [{
        p: "Friendliest food in the neighborhood ",
        p2: "Megobar is a new chain of food shops wish a mission to make <br /> delicious Georgian food accessible to everyone around the world. <br /> Megobar (mdmn) means 'a friend' in Georgian, and originally only <br /> referred to people you share a meal with, proving that food and <br /> friendship are colossally important to our culture.",
        image: OurWORKSImage1,
        alt: "Image 1",
        imageText: "Megobar - Georgian",
        imageText2: "Food Shop"
      },
      {
        p2: "Blauenstein is a Swiss-Georgian company creating the finest meat <br /> products in pristine highlands of Racha, Georgia. With a culture of <br /> respect to nature and local traditions, Swiss-trained professionals and <br /> an absolute control over the entire chain of production, Blauenstein <br /> shops are always full of meat connoisseurs.",
        image: OurWORKSImage2,
        alt: 'Image 2',
        imageText: 'BLAUENSTEIN FARM'
      },
      {
        p2: "Out of nothing comes the brand new visual identity for CCLA, Tbilisi- <br /> based law consulting agency which uses creativity to open right doors <br /> for its clients.",
        image: OurWORKSImage3,
        alt: 'Image 3',
        imageText: 'CCLA - LAW CONSULTING AGENCY',
        imageText2: 'Consuling Agency'
      },
      {
        p: "This is not Harper’s Bazaar. The exclusive issue of Women From The <br /> Bazaar unites six trader women from Tbilisi's open-air markets.",
        p2: " In addition to working 70 hours a week, trader women are often <br /> synonymous with waist bags, which are used as self-made cash <br /> registers. In collaboration with Cosmo, a handmade accessories <br /> brand, we decided to launch an extraordinary fashion magazine about <br /> universal, everyday fashion.",
        image: OurWORKSImage4,
        alt: 'Image 4',
        imageText: 'Women From',
        imageText2: 'The Baazar'
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

  .mob {
    width: 300px;
    position: relative;
    bottom: 500px;
  }

  .imageText-mob {
    bottom: 270px;
  }
}
</style>
