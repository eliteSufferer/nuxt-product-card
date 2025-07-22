<template>
    <div class="product-info">
      <div class="product-header">
        <div class="product-title-row">
          <h1 class="product-title">{{ title }}</h1>
          <button class="product-favorite-icon" aria-label="Добавить в избранное">
            <IconFavorite />
          </button>
        </div>
        <div class="product-price">{{ price.current }}</div>
      </div>
  
      <div class="product-section">
        <h3 class="section-title">Размеры</h3>
        <div class="sizes">
          <div 
            v-for="size in sizes" 
            :key="size.id"
            class="size-item"
          >
            <button 
              :class="['size-btn', { 
                'size-btn--active': selectedSize === size.id,
                'size-btn--disabled': !size.available 
              }]"
              :disabled="!size.available"
              @click="selectSize(size.id)"
            >
              {{ size.label }}
            </button>
            <div v-if="size.stock" class="size-stock">{{ size.stock }}</div>
          </div>
        </div>
      </div>
  
      <div class="product-section">
        <h3 class="section-title">Цвет: {{ selectedColorName }}</h3>
        <div class="colors">
          <button
            v-for="color in colors"
            :key="color.id"
            :class="['color-btn', { 'color-btn--active': selectedColor === color.id }]"
            :style="{ backgroundColor: color.color }"
            @click="selectColor(color.id)"
            :aria-label="`Выбрать цвет ${color.label}`"
          />
        </div>
      </div>
  
      <div class="product-actions">
        <button class="btn btn-primary product-buy-btn">
          Добавить в корзину
        </button>
        <button class="btn product-favorite-btn product-favorite-btn--desktop" style="background: transparent; border: 1px solid var(--black-dark)">
          <IconFavorite />
        </button>
      </div>
  
      <div class="product-accordions">
        <ProductAccordion 
          title="Описание"
          :content="description"
          :isOpen="openAccordion === 'description'"
          @toggle="toggleAccordion('description')"
        />
        <ProductAccordion 
          title="Состав и уход"
          :content="composition"
          :isOpen="openAccordion === 'composition'"
          @toggle="toggleAccordion('composition')"
        />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ProductInfo',
    
    props: {
      title: {
        type: String,
        required: true
      },
      price: {
        type: Object,
        required: true
      },
      sizes: {
        type: Array,
        default: () => []
      },
      colors: {
        type: Array,
        default: () => []
      },
      description: {
        type: String,
        default: ''
      },
      composition: {
        type: String,
        default: ''
      }
    },
    
    data() {
      return {
        selectedSize: null,
        selectedColor: null,
        openAccordion: null
      }
    },
    
    computed: {
      selectedColorName() {
        const color = this.colors.find(c => c.id === this.selectedColor)
        return color ? color.label : ''
      }
    },
    
    mounted() {
      const firstAvailableSize = this.sizes.find(s => s.available)
      if (firstAvailableSize) {
        this.selectedSize = firstAvailableSize.id
      }
      
      const activeColor = this.colors.find(c => c.active)
      if (activeColor) {
        this.selectedColor = activeColor.id
      }
    },
    
    methods: {
      selectSize(sizeId) {
        this.selectedSize = sizeId
      },
      
      selectColor(colorId) {
        this.selectedColor = colorId
      },
      
      toggleAccordion(accordionId) {
        this.openAccordion = this.openAccordion === accordionId ? null : accordionId
      }
    }
  }
  </script>
  
  <style scoped>
  .product-info {
    width: 100%;
    max-width: 360px;
  }
  
  .product-header {
    margin-bottom: 32px;
  }
  
  .product-title-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 8px;
  }
  
  .product-title {
    font-size: 12px;
    line-height: 16px;
    font-weight: 400;
    text-transform: uppercase;
    color: var(--black-middle);
    margin: 0;
  }
  
  .product-favorite-icon {
    display: none;
    background: none;
    border: none;
    cursor: pointer;
    width: 20px;
    height: 20px;
    color: var(--black-dark);
    transition: opacity 0.2s ease;
  }
  
  .product-favorite-icon:hover {
    opacity: 0.7;
  }
  
  .product-price {
    font-size: 12px;
    line-height: 16px;
    font-weight: 400;
    text-transform: uppercase;
    color: var(--black-middle);
  }
  
  .product-section {
    margin-bottom: 32px;
  }
  
  .section-title {
    font-size: 10px;
    line-height: 14px;
    font-weight: 400;
    color: var(--gray-dark);
    margin-bottom: 16px;
  }
  
  .sizes {
    display: flex;
    gap: 16px;
    margin-bottom: 16px;
  }
  
  .size-item {
    position: relative;
  }
  
  .size-btn {
    width: 65px;
    height: 31px;
    border: 1px solid var(--black-middle);
    background: transparent;
    font-size: 10px;
    line-height: 14px;
    font-weight: 400;
    text-transform: uppercase;
    color: var(--black-middle);
    cursor: pointer;
    transition: all 0.2s ease;
  }
  
  .size-btn--active {
    background: var(--black-dark);
    color: var(--white);
    border-color: var(--black-dark);
  }
  
  .size-btn--disabled {
    border-color: var(--gray-light);
    color: var(--gray-light);
    cursor: not-allowed;
  }
  
  .size-stock {
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translateX(-50%);
    margin-top: 4px;
    font-size: 10px;
    line-height: 14px;
    color: var(--gray-middle);
    white-space: nowrap;
  }
  
  .colors {
    display: flex;
    gap: 16px;
    margin-bottom: 16px;
  }
  
  .color-btn {
    width: 28px;
    height: 27px;
    border: 1px solid var(--gray-light);
    cursor: pointer;
    position: relative;
    transition: all 0.2s ease;
  }
  
  .color-btn--active::after {
    content: '';
    position: absolute;
    bottom: -8px;
    left: 50%;
    transform: translateX(-50%);
    width: 34px;
    height: 1px;
    background: var(--gray-dark);
  }
  
  .product-actions {
    display: flex;
    gap: 10px;
    margin-bottom: 48px;
  }
  
  .product-buy-btn {
    flex: 1;
    font-size: 11px;
    line-height: 15px;
  }
  
  .product-favorite-btn {
    width: 44px;
  }
  
  .product-accordions {
    border-top: 1px solid var(--gray-lighter);
  }
  
  @media (max-width: 768px) {
    .product-info {
      max-width: none;
    }
    
    .product-favorite-icon {
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    .product-actions {
      display: none;
    }
    
    .sizes {
      gap: 12px;
    }
    
    .size-btn {
      width: 55px;
      height: 28px;
      font-size: 9px;
    }
  }
  </style>