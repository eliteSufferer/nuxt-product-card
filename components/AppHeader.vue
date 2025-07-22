<template>
    <header class="header">
        <div class="container">
            <div class="header__inner">
                <div class="header__logo">
                    <img src="/images/logo.png" alt="STIK" class="header__logo-img" />
                </div>

                <nav class="header__nav">
                    <div class="header__nav-desktop">
                        <button class="header__nav-btn" aria-label="Поиск">
                            <IconSearch />
                        </button>
                        <button class="header__nav-btn" aria-label="Избранное">
                            <IconFavorite />
                        </button>
                        <button class="header__nav-btn" aria-label="Профиль">
                            <IconUser />
                        </button>
                        <button class="header__nav-btn" aria-label="Корзина">
                            <IconBasket />
                        </button>
                    </div>

                    <div class="header__nav-mobile">
                        <div class="header__nav-btn--left">
                            <button class="header__nav-btn" aria-label="Профиль">
                                <IconUser />
                            </button>

                            <button class="header__nav-btn" aria-label="Поиск">
                                <IconSearch />
                            </button>
                        </div>

                        <button class="header__nav-btn header__nav-btn--right" aria-label="Корзина">
                            <IconBasket />
                        </button>
                    </div>
                </nav>
            </div>
        </div>
    </header>
</template>
  
  <script>
  export default {
    name: 'AppHeader'
  }
  </script>
  
  <style scoped>
  .header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: 86px;
    background: var(--white);
    z-index: 100;
  }
  
  .header__inner {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;
    margin-top: 31px;
  }
  
  .header__logo {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }

  .header__logo-img {
    height: 24px;
    width: auto;
  }
  
  .header__nav {
    display: flex;
    align-items: center;
    margin-left: auto;
  }
  
  .header__nav-desktop {
    display: flex;
    align-items: center;
    gap: 16px;
  }
  
  .header__nav-mobile {
    display: none;
    position: absolute;
    width: 100%;
    left: 0;
    top: 50%;
    transform: translateY(-50%);
  }
  
  .header__nav-btn--left {
    position: absolute;
    left: 16px;
    display: flex;
    flex-direction: row;
    gap: 16px;
  }
  
  .header__nav-btn--right {
    position: absolute;
    right: 16px;
  }
  
  .header__nav-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 20px;
    height: 20px;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    transition: opacity 0.2s ease;
  }
  
  .header__nav-btn:hover {
    opacity: 0.7;
  }
  
  @media (max-width: 768px) {
    .header {
      height: 50px;
    }
 
    .header__inner {
      margin-top: 18px;
    }

    .header__logo {
      margin-top: 10px;
    }
    
    .header__nav-desktop {
      display: none;
    }
    
    .header__nav-mobile {
      display: block;
    }
  }
  </style>