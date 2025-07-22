<template>
  <div class="product-page">
    <div class="container">
      <section class="product-section">
        <div class="product-content">
          <ProductGallery :images="productImages"/>
          
          <ProductInfo 
            :title="product.title"
            :price="product.price"
            :sizes="product.sizes"
            :colors="product.colors"
            :description="product.description"
            :composition="product.composition"
            class="product-info"
          />
        </div>
      </section>
      
      <SimilarProducts :products="similarProducts" class="similar-products"/>
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
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse rutrum velit et metus fringilla, a dapibus diam tristique. Nam vitae posuere leo. Cras a consectetur dui. Aliquam tincidunt ipsum mauris, eu semper ligula accumsan vel.',
        composition: 'Morbi velit ipsum, egestas nec tortor ac, dignissim scelerisque nisi. Sed et dui placerat, pretium diam sed, pellentesque tellus.'
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
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `${this.product.title} за ${this.product.price.current}. Купить в интернет-магазине STIK.`
        }
      ]
    }
  }
}
</script>

<style scoped>

.product-section {
  margin-bottom: 80px;
}

.product-content {
  display: grid;
  grid-template-columns: 1fr 700px;
  gap: 10px;
  align-items: start;
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
  .product-section {
    margin-bottom: 40px;
  }
  
  .product-content {
    gap: 30px;
  }
  .container {
    padding: 0;
  }

  .product-info, .similar-products {
    padding: 0 16px;
  }
  
}
</style>