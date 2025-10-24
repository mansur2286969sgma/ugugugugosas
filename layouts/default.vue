<template>
  <div>
    <header class="flex w-full items-center justify-between bg-black shadow-sm py-2 sticky top-0 z-50 text-white">
      <div class="basis-1/4 items-center justify-start px-4 sm:px-10">
        <img class="min-w-[40px] w-10 h-10 flex-shrink-0 object-cover rounded-full" src="/assets/images/water.png" alt="Logo">
      </div>
      
      <!-- Поисковая строка -->
      <div class="basis-1/4 flex justify-center">
        <div class="relative w-48 sm:w-64">
          <input 
            type="text" 
            v-model="searchQuery"
            placeholder="Search..."
            class="w-full px-4 py-2 rounded-full bg-gray-800 text-white border-2 border-[#00CCFF] focus:outline-none focus:border-blue-400 text-sm sm:text-base"
          >
          <div class="absolute right-3 top-1/2 transform -translate-y-1/2">
            <svg class="w-4 h-4 sm:w-5 sm:h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
            </svg>
          </div>
        </div>
      </div>

      <!-- Бургер-кнопка с улучшенным позиционированием -->
      <button class="hidden max-sm:block px-4 text-white focus:outline-none z-60 relative" @click="switchBurger">
        <div v-if="!burger" class="space-y-1">
          <div class="w-6 h-0.5 bg-white"></div>
          <div class="w-6 h-0.5 bg-white"></div>
          <div class="w-6 h-0.5 bg-white"></div>
        </div>
        <div v-else class="relative w-6 h-6">
          <div class="absolute top-1/2 left-1/2 w-6 h-0.5 bg-white transform -translate-x-1/2 -translate-y-1/2 rotate-45"></div>
          <div class="absolute top-1/2 left-1/2 w-6 h-0.5 bg-white transform -translate-x-1/2 -translate-y-1/2 -rotate-45"></div>
        </div>
      </button>
      
      <!-- Навигация с улучшенной адаптацией -->
      <nav class="basis-1/2 flex flex-row items-center justify-end px-4 gap-4 max-sm:fixed max-sm:top-0 max-sm:left-0 max-sm:w-full max-sm:h-screen max-sm:bg-gray-900 max-sm:flex-col max-sm:justify-start max-sm:gap-6 max-sm:pt-24 max-sm:pb-8 max-sm:overflow-y-auto"
           :class="{'max-sm:hidden': !burger}">

        <!-- Кнопка закрытия для мобильной версии -->
        <button 
          v-if="burger"
          class="hidden max-sm:block absolute top-4 right-4 text-white p-2 rounded-full bg-gray-800 border-2 border-[#00CCFF] z-60"
          @click="switchBurger">
          <div class="w-4 h-4 relative">
            <div class="absolute top-1/2 left-1/2 w-4 h-0.5 bg-white transform -translate-x-1/2 -translate-y-1/2 rotate-45"></div>
            <div class="absolute top-1/2 left-1/2 w-4 h-0.5 bg-white transform -translate-x-1/2 -translate-y-1/2 -rotate-45"></div>
          </div>
        </button>

        <NuxtLink to="/" class="my-auto p-3 sm:p-4 hover:bg-gray-100 text-[#00CCFF] text-base sm:text-lg font-medium max-sm:w-11/12 max-sm:text-center max-sm:border-2 max-sm:border-[#00CCFF] max-sm:rounded-lg max-sm:py-3" @click.native="closeMenus">Home</NuxtLink>
        
        <!-- Выпадающее меню Labs -->
        <div class="relative group max-sm:w-11/12">
          <button class="my-auto p-3 sm:p-4 hover:bg-gray-100 text-[#00CCFF] text-base sm:text-lg font-medium max-sm:w-full max-sm:text-center max-sm:border-2 max-sm:border-[#00CCFF] max-sm:rounded-lg max-sm:py-3" 
                  @click="isMobile && switchLabs()">
            Labs ▼
          </button>
          
          <!-- Десктопное подменю -->
          <div class="absolute top-full left-0 bg-gray-900 border-2 border-[#00CCFF] rounded-lg shadow-xl py-2 min-w-48 max-sm:hidden opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-200 z-50">
            <NuxtLink to="/Lab3" class="block p-4 hover:bg-[#00CCFF] hover:text-white border-b border-gray-200 last:border-b-0">Lab3</NuxtLink>
            <NuxtLink to="/Lab4" class="block p-4 hover:bg-[#00CCFF] hover:text-white border-b border-gray-200 last:border-b-0">Lab4</NuxtLink>
            <NuxtLink to="/Lab5" class="block p-4 hover:bg-[#00CCFF] hover:text-white border-b border-gray-200 last:border-b-0">Lab5</NuxtLink>
            <NuxtLink to="/Lab6" class="block p-4 hover:bg-[#00CCFF] hover:text-white border-b border-gray-200 last:border-b-0">Songs</NuxtLink>
          </div>
          
          <!-- Мобильное подменю -->
          <div v-show="labsVisible && burger" class="hidden max-sm:block max-sm:w-full max-sm:mt-2 max-sm:border-2 max-sm:border-[#00CCFF] max-sm:rounded-lg max-sm:bg-gray-800">
            <NuxtLink to="/Lab3" class="block p-4 hover:bg-[#00CCFF] hover:text-white border-b border-gray-200 text-center" @click.native="closeMenus">Lab3</NuxtLink>
            <NuxtLink to="/Lab4" class="block p-4 hover:bg-[#00CCFF] hover:text-white border-b border-gray-200 text-center" @click.native="closeMenus">Lab4</NuxtLink>
            <NuxtLink to="/Lab5" class="block p-4 hover:bg-[#00CCFF] hover:text-white border-b border-gray-200 text-center" @click.native="closeMenus">Lab5</NuxtLink>
            <NuxtLink to="/Lab6" class="block p-4 hover:bg-[#00CCFF] hover:text-white text-center" @click.native="closeMenus">Songs</NuxtLink>
          </div>
        </div>
        
        <NuxtLink to="/login" class="my-auto p-3 sm:p-4 hover:bg-gray-100 text-[#00CCFF] text-base sm:text-lg font-medium max-sm:w-11/12 max-sm:text-center max-sm:border-2 max-sm:border-[#00CCFF] max-sm:rounded-lg max-sm:py-3" @click.native="closeMenus">Login</NuxtLink>
        <NuxtLink to="/logout" class="my-auto p-3 sm:p-4 hover:bg-gray-100 text-[#00CCFF] text-base sm:text-lg font-medium max-sm:w-11/12 max-sm:text-center max-sm:border-2 max-sm:border-[#00CCFF] max-sm:rounded-lg max-sm:py-3" @click.native="closeMenus">LogOut</NuxtLink>
      </nav>
    </header>

    <!-- Основной контент с отступом для мобильного меню -->
    <main class="p-4 sm:p-5 flex bg-gray-900 min-h-screen mt-0" :class="{'max-sm:mt-0': !burger}">
      <slot /> 
    </main>

    <footer class="w-full bg-gray-900 border-t-2 border-[#00CCFF]">
      <div class="flex items-center justify-center px-4 py-2 gap-3 sm:gap-4">
        <a href="https://app.netlify.com/projects/water229/configuration/general"><img src="/assets/images/netlify.png" class="w-12 h-12 sm:w-16 sm:h-16"></a>
        <a href="https://github.com/mansur2286969sgma/ugugugugosas"><img src="/assets/images/github.png" class="w-12 h-12 sm:w-16 sm:h-16"></a>
        <a href="https://analytics.google.com/analytics/web/#/a368958209p505673999/reports/intelligenthome?params=_u..nav%3Dmaui"><img src="/assets/images/analytics.png" class="w-12 h-12 sm:w-16 sm:h-16"></a>
      </div>
      <div class="w-full bg-gray-900 border-t-2 border-[#00CCFF]">
        <div class="text-xs text-gray-500 text-center py-2">
          <p>2025 Mansur corp.</p>
          <p>All rights reserved</p>
        </div>
      </div>
    </footer>
  </div>
</template>
<script>
export default {
  data() {
    return {
      burger: false,
      labsVisible: false,
      isMobile: false,
      searchQuery: ''
    }
  },
  methods: {
    switchBurger() {
      this.burger = !this.burger
      // Закрываем подменю Labs при открытии/закрытии бургера
      this.labsVisible = false
    },
    switchLabs() {
      this.labsVisible = !this.labsVisible
    },
    closeMenus() {
      this.burger = false
      this.labsVisible = false
    },
    checkMobile() {
      this.isMobile = window.innerWidth <= 480
    },
    handleResize() {
      this.checkMobile()
      // Закрываем меню при изменении размера на десктоп
      if (!this.isMobile) {
        this.burger = false
        this.labsVisible = false
      }
    }
  },
  mounted() {
    this.checkMobile()
    window.addEventListener('resize', this.handleResize)
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize)
  },
  watch: {
    $route() {
      this.closeMenus()
    }
  },
  head() {
    return {
      script: [
        {
          src: 'https://www.googletagmanager.com/gtag/js?id=G-MPRBV4HM0D',
          async: true
        },
        {
          innerHTML: `
            window.dataLayer = window.dataLayer || [];
            function gtag(){dataLayer.push(arguments);}
            gtag('js', new Date());
            gtag('config', 'G-MPRBV4HM0D');
          `,
          type: 'text/javascript',
          charset: 'UTF-8'
        }
      ]
    }
  }
}
</script>