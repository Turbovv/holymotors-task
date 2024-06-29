<template>
  <div>
    <Carousel
      :slides="slidesData"
      class="bg-red-500"
      variant="variant2"
      progressBars="flex  justify-center top-16   relative items-center gap-4 z-10"
      imageText="text-white text-lg md:text-4xl uppercase bg-black items-center  p-2 md:p-4"
      nextButtonClass="bg-black bg-opacity-50 text-white p-1 w-5 cursor-pointer"
      prevButtonClass="bg-black bg-opacity-50 text-white p-1 w-5 cursor-pointer"
      progressBarsClass="4"
      pClass="font-light tracking-wide text-2xl mb-6 md:mb-10 xl:mb-16 leading-8"
      ptwoClass="font-light tracking-wide text-lg md:text-xl xl:text-3xl mb-6 md:mb-10 xl:mb-16 leading-8"
      textContainerClass="text-left w-full p-6 text-white order-2 border border-black md:order-1"
      imageContainerClass="p-6 order-1 md:order-2"
      buttonsClass="buttons justify- flex relative items-center bottom-16"
      slideNumberClass="relative test text-black  text-lg md:text-2xl"
    />
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
      slidesData: [
        {
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
  }
};
</script>

<style scoped>
.test {
  border:1px solid black;
}
</style>