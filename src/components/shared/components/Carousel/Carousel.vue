<template>
  <div :class="[variantClass]" @mousedown="startDrag" @mousemove="dragging" @mouseup="endDrag" @mouseleave="endDrag"
    @touchstart="startDrag" @touchmove="dragging" @touchend="endDrag" @touchcancel="endDrag">
    <div :class="[progressBarsClass]">
      <div :class="[progressBars]">
        <div v-for="(bar, index) in progressBarData" :key="index" class="progress-bar h-1.5 bg-gray-200"
          :class="{ '': index < progressBarData.length - 1 }" :style="{ width: bar.width }">
          <div class="progress h-full" :style="{ width: `${bar.innerWidth}%`, backgroundColor: bar.color }"></div>
        </div>
      </div>
    </div>
    <div class="embla__viewport" ref="viewport">
      <div class="embla__container">
        <div v-for="(slide, index) in slides" :key="index" :class="['embla__slide', variantClass, dflex]">
          <slot name="slide-content" :slide="slide" :index="index" :current-index="currentIndex"></slot>
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
    prevButtonClass: {
      type: String,
      default: ''
    },
    dflex: {
      type: String,
      default: ''
    },
    progressBarsClass: {
      type: String,
      default: ''
    },
    progressBars: {
      type: String,
      default: ''
    },
    h1Class: {
      type: String,
      default: ''
    },
    pClass: {
      type: String,
      default: ''
    },
    ptwoClass: {
      type: String,
      default: ''
    },
    imageText: {
      type: String,
      default: ''
    },
    textContainerClass: {
      type: String,
      default: ''
    },
    imageContainerClass: {
      type: String,
      default: ''
    },
    buttonsClass: {
      type: String,
      default: ''
    },
    slideNumberClass: {
      type: String,
      default: ''
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
      const progressPerBar = totalSlides / this.progressBarsClass;

      this.progressBarData = Array.from({
        length: this.progressBarsClass
      }, (_, i) => {
        const startSlideIndex = progressPerBar * i + 1;
        const endSlideIndex = progressPerBar * (i + 1);
        const isActive = currentSlideIndex >= startSlideIndex && currentSlideIndex <= endSlideIndex;
        const width = 400;
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
    this.autoSlide = setInterval(this.nextSlide, 2500);
  },
  beforeUnmount() {
    clearInterval(this.autoSlide);
    this.embla.destroy();
  }
};
</script>

<style scoped>
.embla__container {
  display: flex;
}
</style>
