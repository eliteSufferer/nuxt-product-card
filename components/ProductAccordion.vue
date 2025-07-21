<template>
    <div class="accordion">
      <button 
        class="accordion__header"
        @click="$emit('toggle')"
        :aria-expanded="isOpen"
      >
        <span class="accordion__title">{{ title }}</span>
        <IconPlus :class="['accordion__icon', { 'accordion__icon--open': isOpen }]" />
      </button>
      
      <div 
        v-if="isOpen" 
        class="accordion__content"
      >
        <div class="accordion__text">
          {{ content }}
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ProductAccordion',
    
    props: {
      title: {
        type: String,
        required: true
      },
      content: {
        type: String,
        default: ''
      },
      isOpen: {
        type: Boolean,
        default: false
      }
    },
    
    emits: ['toggle']
  }
  </script>
  
  <style scoped>
  .accordion {
    border-bottom: 1px solid var(--gray-lighter);
  }
  
  .accordion__header {
    width: 100%;
    height: 41px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    position: relative;
  }
  
  .accordion__title {
    font-size: 10px;
    line-height: 14px;
    font-weight: 400;
    text-transform: uppercase;
    color: var(--black-middle);
  }
  
  .accordion__icon {
    width: 12px;
    height: 12px;
    color: var(--gray-middle);
    transition: transform 0.2s ease;
  }
  
  .accordion__icon--open {
    transform: rotate(45deg);
  }
  
  .accordion__content {
    padding-bottom: 16px;
    animation: slideDown 0.2s ease;
  }
  
  .accordion__text {
    font-size: 10px;
    line-height: 14px;
    color: var(--black-middle);
  }
  
  @keyframes slideDown {
    from {
      opacity: 0;
      transform: translateY(-10px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  </style>