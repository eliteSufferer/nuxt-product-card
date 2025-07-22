<template>
  <div class="gallery">
    <div class="gallery__thumbs">
      <button
        v-for="(image, index) in images"
        :key="image.id"
        :class="['gallery__thumb', { 'gallery__thumb--active': index === activeIndex }]"
        @click="setActiveImage(index)"
      >
        <img :src="image.src" :alt="image.alt" class="gallery__thumb-img" />
      </button>
    </div>

    <div class="gallery__main">
      <div class="gallery__container">
        <button 
          class="gallery__nav gallery__nav--prev"
          @click="prevImage"
          :disabled="activeIndex === 0"
        >
          <IconArrowLeft />
        </button>
        
        <button 
          class="gallery__nav gallery__nav--next"
          @click="nextImage"
          :disabled="activeIndex === images.length - 1"
        >
          <IconArrowRight />
        </button>

        <div 
          class="gallery__image-wrapper"
          @touchstart="handleTouchStart"
          @touchmove="handleTouchMove"
          @touchend="handleTouchEnd"
        >
          <img 
            :src="currentImage.src" 
            :alt="currentImage.alt"
            class="gallery__main-img"
          />
        </div>

        <div class="gallery__dots gallery__dots--mobile">
          <button
            v-for="(image, index) in images"
            :key="`dot-${image.id}`"
            :class="['gallery__dot', { 'gallery__dot--active': index === activeIndex }]"
            @click="setActiveImage(index)"
            :aria-label="`Показать изображение ${index + 1}`"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductGallery',
  
  props: {
    images: {
      type: Array,
      default: () => []
    }
  },
  
  data() {
    return {
      activeIndex: 0,
      touchStartX: 0,
      touchEndX: 0
    }
  },
  
  computed: {
    currentImage() {
      return this.images[this.activeIndex] || {}
    }
  },
  
  methods: {
    setActiveImage(index) {
      this.activeIndex = index
    },
    
    prevImage() {
      if (this.activeIndex > 0) {
        this.activeIndex--
      }
    },
    
    nextImage() {
      if (this.activeIndex < this.images.length - 1) {
        this.activeIndex++
      }
    },

    handleTouchStart(e) {
      this.touchStartX = e.touches[0].clientX
    },

    handleTouchMove(e) {
      this.touchEndX = e.touches[0].clientX
    },

    handleTouchEnd() {
      const swipeThreshold = 50
      const swipeDistance = this.touchStartX - this.touchEndX

      if (Math.abs(swipeDistance) > swipeThreshold) {
        if (swipeDistance > 0) {
          this.nextImage()
        } else {
          this.prevImage()
        }
      }
    }
  }
}
</script>

<style scoped>
.gallery {
  display: flex;
  gap: 30px;
  position: relative;
}

.gallery__thumbs {
  display: flex;
  flex-direction: column;
  gap: 4px;
  width: 70px;
  flex-shrink: 0;
}

.gallery__thumb {
  width: 70px;
  height: 88px;
  border: none;
  padding: 0;
  cursor: pointer;
  background: none;
  position: relative;
  overflow: hidden;
}

.gallery__thumb--active .gallery__thumb-img {
  opacity: 0.5;
}

.gallery__thumb-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: opacity 0.2s ease;
}

.gallery__thumb:hover .gallery__thumb-img {
  opacity: 0.7;
}

.gallery__main {
  flex: 1;
  position: relative;
}

.gallery__container {
  position: relative;
  width: 518px;
  height: 693px;
  overflow: hidden;
}

.gallery__image-wrapper {
  width: 100%;
  height: 100%;
}

.gallery__main-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.gallery__nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 32px;
  height: 32px;
  border: none;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.4);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
  transition: background-color 0.2s ease;
}

.gallery__nav:hover:not(:disabled) {
  background: rgba(255, 255, 255, 0.6);
}

.gallery__nav:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

.gallery__nav--prev {
  left: 16px;
}

.gallery__nav--next {
  right: 16px;
}

.gallery__dots {
  display: none;
  position: absolute;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  gap: 8px;
  z-index: 2;
}

.gallery__dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.5);
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.gallery__dot--active {
  background: rgba(255, 255, 255, 0.9);
}

@media (max-width: 768px) {
  .gallery {
    flex-direction: column;
    gap: 0;
  }
  
  .gallery__thumbs {
    display: none;
  }
  
  .gallery__dots--mobile {
    display: flex;
  }
  
  .gallery__container {
    width: 100%;
    height: auto;
    min-height: 300px;
  }
  
  .gallery__image-wrapper {
    width: 100%;
    height: auto;
  }
  
  .gallery__main-img {
    width: 100%;
    height: auto;
    object-fit: contain;
    max-height: 70vh;
  }
  
  .gallery__nav {
    top: 40%;
  }
}
</style>