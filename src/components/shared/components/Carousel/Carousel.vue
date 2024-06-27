<template>
  <div :class="[variantClass]" @mousedown="startDrag" @mousemove="dragging" @mouseup="endDrag" @mouseleave="endDrag"
    @touchstart="startDrag" @touchmove="dragging" @touchend="endDrag" @touchcancel="endDrag">
    <div class="progress-bars flex w-full md:w-5/12 float-right top-12 right-4 md:right-20 relative items-center gap-4 z-10">
      <div v-for="(bar, index) in progressBarData" :key="index" class="progress-bar h-1 bg-gray-200"
        :class="{ '': index < progressBarData.length - 1 }" :style="{ width: bar.width }">
        <div class="progress h-full" :style="{ width: `${bar.innerWidth}%`, backgroundColor: bar.color }"></div>
      </div>
    </div>
    <div class="embla__viewport" ref="viewport">
      <div class="embla__container">
        <div v-for="(slide, index) in slides" :key="index"
          :class="['embla__slide carousel-item flex flex-col md:flex-row', variantSlideClass]">
          <div class="w-full md:w-1/2 p-6 order-1 md:order-2">
            <img :src="slide.image" :alt="slide.alt" :class="['w-full h-auto', imageClass]" />
            <div class="buttons justify-between flex relative items-center bottom-16">
              <div class="slide-number text-red-500 text-lg md:text-2xl">
                0{{ currentIndex + 1 }}
              </div>
              <div class="gap-4 flex">
                <button
                  :class="['carousel-control relative bg-red-500 bg-opacity-50 text-white p-1 w-5 cursor-pointer', prevButtonClass]"
                  @click="prevSlide">
                  &#10094;
                </button>
                <button
                  :class="['carousel-control relative bg-red-500 bg-opacity-50 text-white p-1 w-5 cursor-pointer', nextButtonClass]"
                  @click="nextSlide">
                  &#10095;
                </button>
              </div>
              <div class="text-white text-lg md:text-4xl uppercase bg-black items-center border p-2 md:p-4 border-red-500">
                <h1>{{ slide.imageText }}</h1>
              </div>
            </div>
          </div>
          <div class="text-left w-full md:w-1/2 p-6 text-white order-2 md:order-1">
            <div class="pl-6 h-full">
              <h1 v-html="slide.h1" class="uppercase font-extralight h1Class text-2xl md:text-3xl xl:text-5xl mb-6 md:mb-10 xl:mb-16 leading-8"></h1>
              <p v-html="slide.p" class="font-light tracking-wide pClass text-lg md:text-xl xl:text-3xl mb-6 md:mb-10 xl:mb-16 leading-8"></p>
              <p v-html="slide.p2" class="font-light tracking-wide text-lg md:text-xl xl:text-3xl mb-6 md:mb-10 xl:mb-16 leading-8"></p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import EmblaCarousel from 'embla-carousel';

export default {
  props: {
    slides: {
      type: Array,
      required: true
    },
    variant: {
      type: String,
      default: 'default'
    },
    imageClass: {
      type: String,
      default: ''
    },
    nextButtonClass: {
      type: String,
      default: ''
    },
    divCarousel: {
      type: String,
      default: ''
    },
    prevButtonClass: {
      type: String,
      default: ''
    },
    progressBars: {
      type: String,
      default: ''
    },
    pClass: {
      type: String,
      default: ""
    },
    ImageSwitchButtons: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      currentIndex: 0,
      progressBarData: [],
      isDragging: false,
      startPosition: 0,
      embla: null
    };
  },
  computed: {
    variantClass() {
      return {
        'carousel-variant-1': this.variant === 'variant1',
        'carousel-variant-2': this.variant === 'variant2',
        'carousel-variant-3': this.variant === 'variant3',
        'carousel-variant-4': this.variant === 'variant4'
      };
    },
    variantSlideClass() {
      return {
        'carousel-slide-variant-1': this.variant === 'variant1',
        'carousel-slide-variant-2': this.variant === 'variant2',
        'carousel-slide-variant-3': this.variant === 'variant3',
        'carousel-slide-variant-4': this.variant === 'variant4'
      };
    }
  },
  methods: {
    startDrag(event) {
      event.preventDefault();
      this.isDragging = true;
      this.startPosition = this.getEventPosition(event);
    },
    dragging(event) {
      event.preventDefault();
      if (this.isDragging) {
        const currentPosition = this.getEventPosition(event);
        const difference = currentPosition - this.startPosition;
        if (Math.abs(difference) > 50) {
          difference > 0 ? this.prevSlide() : this.nextSlide();
          this.isDragging = false;
        }
      }
    },
    endDrag() {
      this.isDragging = false;
    },
    getEventPosition(event) {
      return event.type.includes('touch') ? event.touches[0].clientX : event.clientX;
    },
    showSlide(index) {
      this.currentIndex = index;
      this.embla.scrollTo(index);
      this.updateProgressBars();
    },
    updateProgressBars() {
      const totalSlides = this.slides.length;
      const currentSlideIndex = this.currentIndex + 1;
      const progressPerBar = totalSlides / this.progressBars;

      this.progressBarData = Array.from({ length: this.progressBars }, (_, i) => {
        const startSlideIndex = progressPerBar * i + 1;
        const endSlideIndex = progressPerBar * (i + 1);
        const isActive = currentSlideIndex >= startSlideIndex && currentSlideIndex <= endSlideIndex;
        const width = 300;
        const remaining = Math.max(0, currentSlideIndex - startSlideIndex + 1);
        const innerWidth = (remaining / progressPerBar) * 100;
        return {
          width: `${width}px`,
          innerWidth: isActive ? innerWidth : 0,
          color: isActive ? 'red' : 'transparent'
        };
      });
    },
    nextSlide() {
      const nextIndex = (this.currentIndex + 1) % this.slides.length;
      this.showSlide(nextIndex);
    },
    prevSlide() {
      const prevIndex = (this.currentIndex - 1 + this.slides.length) % this.slides.length;
      this.showSlide(prevIndex);
    }
  },
  mounted() {
    const options = {};
    this.embla = EmblaCarousel(this.$refs.viewport, options);
    this.embla.on('select', () => {
      this.currentIndex = this.embla.selectedScrollSnap();
      this.updateProgressBars();
    });
    this.updateProgressBars();
    // this.autoSlide = setInterval(this.nextSlide, 5000);
  },
  beforeUnmount() {
    clearInterval(this.autoSlide);
    this.embla.destroy();
  }
};
</script>

<style scoped>
.carousel-inner {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-item {
  min-width: 100%;
  transition: opacity 0.5s ease-in-out;
}

.embla__viewport {
  overflow: hidden;
  width: 100%;
}

.embla__container {
  display: flex;
}

.embla__slide {
  flex: 0 0 100%;
}

@media (max-width: 768px) {
  .h1Class {
    font-size: 1.5rem; /* Adjust font size */
    line-height: 2rem;
    margin-bottom: 1.5rem; /* Adjust margin-bottom */
  }
  .pClass {
    font-size: 1.25rem; /* Adjust font size */
    line-height: 1.75rem;
    margin-bottom: 1.5rem; /* Adjust margin-bottom */
  }
  .text-4xl {
    font-size: 1.75rem; /* Adjust font size */
    margin-bottom: 1.5rem; /* Adjust margin-bottom */
  }
}

/* Variant Styles */
.carousel-variant-1 {
  /* Add styles for variant 1 */
}

.carousel-variant-2 {
  color: white;
  text-align: center;
  align-items: center;
}

.carousel-slide-variant-1 {
  /* Add styles for slides in variant 1 */
}

.carousel-slide-variant-2 {
  /* Add styles for slides in variant 2 */
}

.carousel-control {
  /* Add styles for carousel control */
}
</style>
