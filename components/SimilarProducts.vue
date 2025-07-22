<template>
    <section class="similar-products">
      <h2 class="similar-products__title">похожие товары</h2>
      
      <div class="similar-products__grid">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
          @click="handleProductClick(product)"
        />
      </div>
    </section>
  </template>
  
  <script>
  export default {
    name: 'SimilarProducts',
    
    props: {
      products: {
        type: Array,
        default: () => []
      }
    },
    
    methods: {
      handleProductClick(product) {
        console.log('Clicked product:', product)
      }
    }
  }
  </script>
  
  <style scoped>
  .similar-products {
    padding: 40px 0;
  }
  
  .similar-products__title {
    font-size: 12px;
    line-height: 16px;
    font-weight: 400;
    text-transform: uppercase;
    color: var(--black-middle);
    margin-bottom: 25px;
  }
  
  .similar-products__grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 24px;
  }
  
  @media (max-width: 1200px) {
    .similar-products__grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }
  
  @media (max-width: 768px) {
    .similar-products {
      padding: 20px 0;
    }
    
    .similar-products__grid {
      grid-template-columns: repeat(2, 1fr);
      gap: 16px;
    }

  }
  
  @media (max-width: 480px) {
    .similar-products__grid {
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
    }
  }
  </style>