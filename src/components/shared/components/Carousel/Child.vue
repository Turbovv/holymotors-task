<template>
  <div
    class="carousel relative w-full max-w-lg mx-auto overflow-hidden rounded-lg shadow-lg"
    @mousedown="startDrag"
    @mousemove="dragging"
    @mouseup="endDrag"
    @mouseleave="endDrag"
    @touchstart="startDrag"
    @touchmove="dragging"
    @touchend="endDrag"
    @touchcancel="endDrag"
  >
    <div class="progress-bars flex justify-between mb-2">
      <div
        v-for="(bar, index) in progressBarData"
        :key="index"
        class="progress-bar h-1 bg-gray-300"
        :class="{ 'mr-2': index < progressBarData.length - 1 }"
        :style="{ width: bar.width }"
      >
        <div class="progress h-full" :style="{ width: `${bar.innerWidth}%`, backgroundColor: bar.color }"></div>
      </div>
    </div>
    <div
      class="carousel-inner flex transition-transform duration-500"
      :style="{ transform: `translateX(${-currentIndex * 100}%)` }"
    >
      <div v-for="(slide, index) in slides" :key="index" class="carousel-item w-full flex items-center">
        <div class="text-left w-1/2 p-4">
          <p>{{ slide.text }}</p>
        </div>
        <div class="w-1/2">
          <img :src="slide.image" :alt="slide.alt" class="w-full">
        </div>
      </div>
    </div>
    <button
      class="carousel-control absolute top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 text-white p-2 cursor-pointer left-2"
      @click="prevSlide"
    >
      &#10094;
    </button>
    <button
      class="carousel-control absolute top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 text-white p-2 cursor-pointer right-2"
      @click="nextSlide"
    >
      &#10095;
    </button>
    <div
      class="slide-number absolute bottom-2 right-2 bg-black bg-opacity-50 text-white py-1 px-2 rounded-md text-lg"
    >
      {{ currentIndex + 1 }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    slides: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      currentIndex: 0,
      progressBars: 3,
      progressBarData: [],
      isDragging: false,
      startPosition: 0
    };
  },
  computed: {
    progressBarWidth() {
      return '300px';
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
      const totalSlides = this.slides.length;
      this.currentIndex = (index + totalSlides) % totalSlides;
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
      this.showSlide(this.currentIndex + 1);
    },
    prevSlide() {
      this.showSlide(this.currentIndex - 1);
    }
  },
  mounted() {
    this.updateProgressBars();
    this.autoSlide = setInterval(this.nextSlide, 3000);
  },
  beforeUnmount() {
    clearInterval(this.autoSlide);
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
</style>
