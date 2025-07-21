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
  
          <div class="gallery__image-wrapper">
            <img 
              :src="currentImage.src" 
              :alt="currentImage.alt"
              class="gallery__main-img"
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
        activeIndex: 0
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
  
  @media (max-width: 768px) {
    .gallery {
      flex-direction: column-reverse;
      gap: 16px;
    }
    
    .gallery__thumbs {
      flex-direction: row;
      width: auto;
      overflow-x: auto;
      padding-bottom: 4px;
    }
    
    .gallery__thumb {
      flex-shrink: 0;
    }
    
    .gallery__container {
      width: 100%;
      height: 400px;
    }
  }
  </style>