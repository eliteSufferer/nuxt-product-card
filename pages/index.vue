<template>
  <div class="product-page">
    <div class="container">
      <section class="product-section">
        <div class="product-content">
          <ProductGallery :images="productImages" />
          
          <ProductInfo 
            :title="product.title"
            :price="product.price"
            :sizes="product.sizes"
            :colors="product.colors"
            :description="product.description"
            :composition="product.composition"
          />
        </div>
      </section>
      
      <SimilarProducts :products="similarProducts" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductPage',
  
  data() {
    return {
      product: {
        title: 'Жакет удлинённый, белый',
        price: {
          current: '8900 RUB',
          original: null
        },
        sizes: [
          { id: 'xs', label: 'XS', available: true, stock: 'мало' },
          { id: 's', label: 'S', available: true, stock: null },
          { id: 'm', label: 'M', available: false, stock: 'подписка' }
        ],
        colors: [
          { id: 'white', label: 'белый', color: '#FFFFFF', active: true },
          { id: 'black', label: 'черный', color: '#000000', active: false },
          { id: 'cream', label: 'кремовый', color: '#F9F1DC', active: false }
        ],
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer sed mauris augue. Duis sodales nisl sed volutpat bibendum. Nulla laoreet rhoncus magna, ut vestibulum purus congue sed. Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
        composition: 'Ut blandit dui ex. Nulla consectetur rutrum massa, a aliquam ante pulvinar eu. Sed non efficitur leo.'
      },
      
      productImages: [
        { 
          id: 1, 
          src: '/images/jacket-1.png',
          alt: 'Жакет удлинённый вид 1' 
        },
        { 
          id: 2, 
          src: '/images/jacket-2.png',
          alt: 'Жакет удлинённый вид 2' 
        },
        { 
          id: 3, 
          src: '/images/jacket-3.png',
          alt: 'Жакет удлинённый вид 3' 
        }
      ],
      
      similarProducts: [
        {
          id: 1,
          title: 'ПЛАТЬЕ С V-ОБРАЗНЫМ ВЫРЕЗОМ, БЕЛЫЙ',
          price: { current: '14 900 RUB', original: '8 000 RUB' },
          image: '/images/v-shape.png'
        },
        {
          id: 2,
          title: 'ЖАКЕТ ДВУБОРТНЫЙ, СЕРО-ГОЛУБОЙ',
          price: { current: '8900 RUB', original: null },
          image: '/images/jacket-two-sided.png'
        },
        {
          id: 3,
          title: 'ПЛАТЬЕ МАКСИ С ЯРУСАМИ, БЕЛЫЙ',
          price: { current: '10 500 RUB', original: null },
          image: '/images/maxi-dress.png'
        },
        {
          id: 4,
          title: 'КОМБИНЕЗОН СО СТОЙКОЙ, ЧёРНЫЙ',
          price: { current: '9500 RUB', original: null },
          image: '/images/suit-comb.png'
        }
      ]
    }
  },

  head() {
    return {
      title: `${this.product.title} - STIK`,
    }
  }
}
</script>

<style scoped>
.product-page {
  padding: 40px 0;
}

.product-section {
  margin-bottom: 80px;
}

.product-content {
  display: grid;
  grid-template-columns: 1fr 400px;
  gap: 60px;
  align-items: start;
}

.product-info-placeholder {
  padding: 20px;
  background: #f9f9f9;
  border: 1px solid #eee;
}

.product-info-placeholder h1 {
  font-size: 18px;
  margin-bottom: 10px;
  text-transform: uppercase;
}

.price {
  font-size: 14px;
  font-weight: bold;
}

.similar-section h2 {
  font-size: 14px;
  text-transform: uppercase;
  margin-bottom: 20px;
}

.similar-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.similar-item {
  padding: 20px;
  background: #f9f9f9;
  border: 1px solid #eee;
  text-align: center;
}

@media (max-width: 1024px) {
  .product-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
}

@media (max-width: 768px) {
  .product-page {
    padding: 20px 0;
  }
  
  .product-section {
    margin-bottom: 40px;
  }
  
  .product-content {
    gap: 30px;
  }
}
</style>