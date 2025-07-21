<template>
    <article class="product-card" @click="$emit('click', product)">
      <div class="product-card__image">
        <img 
          :src="product.image" 
          :alt="product.title"
          class="product-card__img"
        />
      </div>
      
      <div class="product-card__body">
        <h3 class="product-card__title">{{ product.title }}</h3>
        
        <div class="product-card__price">
          <span class="product-card__price-current">{{ product.price.current }}</span>
          <span 
            v-if="product.price.original"
            class="product-card__price-original"
          >
            {{ product.price.original }}
          </span>
        </div>
      </div>
    </article>
  </template>
  
  <script>
  export default {
    name: 'ProductCard',
    
    props: {
      product: {
        type: Object,
        required: true
      }
    },
    
    emits: ['click']
  }
  </script>
  
  <style scoped>
  .product-card {
    cursor: pointer;
    transition: transform 0.2s ease;
  }
  
  .product-card:hover {
    transform: translateY(-2px);
  }
  
  .product-card__image {
    width: 100%;
    aspect-ratio: 333.49 / 444;
    margin-bottom: 15px;
    overflow: hidden;
  }
  
  .product-card__img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }
  
  .product-card:hover .product-card__img {
    transform: scale(1.05);
  }
  
  .product-card__body {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  
  .product-card__title {
    font-size: 10px;
    line-height: 14px;
    font-weight: 400;
    text-transform: lowercase;
    color: var(--black-middle);
    margin: 0;
  }
  
  .product-card__price {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .product-card__price-current {
    font-size: 10px;
    line-height: 14px;
    font-weight: 400;
    text-transform: uppercase;
    color: var(--black-middle);
  }
  
  .product-card__price-original {
    font-size: 10px;
    line-height: 14px;
    font-weight: 400;
    text-decoration: line-through;
    text-transform: uppercase;
    color: var(--gray-middle);
  }
  
  @media (max-width: 768px) {
    .product-card__image {
      margin-bottom: 12px;
    }
    
    .product-card__body {
      gap: 8px;
    }
  }
  </style>