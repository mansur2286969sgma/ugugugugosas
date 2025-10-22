<template>
  <div class="w-full flex justify-center">
    <div class="max-w-6xl w-full">
      <h1 class="text-3xl font-bold text-center mb-8 text-[#00CCFF]">Music Gallery</h1>
      
      <!-- Radio buttons for selection -->
      <div class="flex flex-wrap justify-center gap-3 md:gap-6 mb-8 px-4">
        <label v-for="option in displayOptions" :key="option.value" class="flex items-center">
          <input 
            type="radio" 
            v-model="selectedOption" 
            :value="option.value" 
            class="hidden"
          >
          <span 
            :class="[
              'px-4 py-2 md:px-6 md:py-3 rounded-full border-2 border-[#00CCFF] text-sm md:text-lg font-medium transition-all duration-300 cursor-pointer whitespace-nowrap',
              selectedOption === option.value 
                ? 'bg-[#00CCFF] text-black shadow-lg shadow-[#00CCFF]/50 transform scale-105' 
                : 'bg-transparent text-[#00CCFF] hover:bg-[#00CCFF] hover:text-black hover:shadow-lg hover:shadow-[#00CCFF]/30 hover:transform hover:scale-105'
            ]"
          >
            {{ option.label }}
          </span>
        </label>
      </div>

      <!-- Images grid using v-for -->
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4 md:gap-6 justify-items-center px-4">
        <div 
          v-for="(item, index) in displayedItems" 
          :key="index"
          class="bg-gray-800 rounded-lg shadow-lg p-3 md:p-4 text-center transition-all duration-300 hover:scale-105 hover:border-2 hover:border-[#00CCFF] w-full max-w-[180px] md:max-w-[200px] border-2 border-transparent relative group"
        >
          <img 
            :src="getImageUrl(item.image)" 
            :alt="item.title"
            class="w-24 h-24 md:w-32 md:h-32 mx-auto object-cover rounded-md mb-2 md:mb-3 border-2 border-[#00CCFF]"
          >
          <h3 class="font-semibold text-white text-base md:text-lg mb-1 leading-tight">{{ item.title }}</h3>
          <p class="text-xs md:text-sm text-[#00CCFF]">{{ item.artist }}</p>
          <p class="text-xs text-gray-400 mt-1 capitalize">{{ item.type }}</p>
          <p v-if="item.feat" class="text-xs text-yellow-400 mt-1">Feat: {{ item.feat }}</p>
          
          <!-- Hover info -->
          <div class="absolute inset-0 bg-black bg-opacity-90 rounded-lg p-4 flex flex-col justify-center items-center opacity-0 group-hover:opacity-100 transition-opacity duration-300">
            <h4 class="text-white font-bold text-lg mb-3 text-center">{{ item.title }}</h4>
            <div class="text-sm text-gray-300 space-y-1 text-center">
              <p><span class="text-[#00CCFF]">Year:</span> {{ item.info.year }}</p>
              <p><span class="text-[#00CCFF]">Genre:</span> {{ item.info.genre }}</p>
              <p><span class="text-[#00CCFF]">Rating:</span> 
                <span class="text-yellow-400">{{ '★'.repeat(item.info.rating) }}{{ '☆'.repeat(5 - item.info.rating) }}</span>
              </p>
              <p v-if="item.info.duration" class="text-gray-400">{{ item.info.duration }}</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Audio player -->
      <div class="max-w-md mx-auto mt-8 md:mt-12 bg-gray-800 rounded-lg shadow-lg p-4 md:p-6 border-2 border-[#00CCFF] mx-4">
        <h2 class="text-xl md:text-2xl font-bold mb-4 md:mb-6 text-center text-[#00CCFF]">Now Playing</h2>
        <audio 
          controls 
          class="w-full rounded-lg bg-gray-700"
        >
          Your browser does not support the audio element.
        </audio>
        <div class="mt-3 md:mt-4 text-center">
          <p class="font-semibold text-white text-lg">herself</p>
          <p class="text-[#00CCFF]">bbno$</p>
          <p class="text-yellow-400 text-sm">Feat: diamond pistols, BENEE</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

// Reactive data
const selectedOption = ref('all')

// Функция для получения URL картинок из assets
const getImageUrl = (imageName) => {
  return new URL(`/assets/images/${imageName}`, import.meta.url).href
}

// Display options for radio buttons
const displayOptions = reactive([
  { label: 'Show All', value: 'all' },
  { label: 'Tame Impala Only', value: 'tame-impala' },
  { label: 'Albums Only', value: 'albums' },
  { label: 'Feats', value: 'feats' },
  { label: 'Other', value: 'other' }
])

// Music items data с дополнительной информацией
const musicItems = reactive([
  { 
    title: 'No Choice', 
    artist: 'Tame Impala', 
    type: 'song', 
    image: 'impala.png',
    info: { year: '2022', genre: 'Psychedelic Pop', rating: 4, duration: '3:42' }
  },
  { 
    title: 'herself', 
    artist: 'bbno$', 
    type: 'song', 
    feat: 'diamond pistols, BENEE', 
    image: 'herself.png',
    info: { year: '2021', genre: 'Pop Rap', rating: 5, duration: '2:51' }
  },
  { 
    title: 'Currents', 
    artist: 'Tame Impala', 
    type: 'album', 
    image: 'impala.png',
    info: { year: '2015', genre: 'Psychedelic Pop', rating: 5, duration: '51:12' }
  },
  { 
    title: 'InnerSpeaker', 
    artist: 'Tame Impala', 
    type: 'album', 
    image: 'impala.png',
    info: { year: '2010', genre: 'Psychedelic Rock', rating: 4, duration: '47:23' }
  },
  { 
    title: 'Fly As Me', 
    artist: 'Bruno Mars', 
    type: 'song', 
    feat: 'Anderson .Paak', 
    image: 'fly.png',
    info: { year: '2021', genre: 'Funk', rating: 4, duration: '3:39' }
  },
  { 
    title: 'Borderline', 
    artist: 'Tame Impala', 
    type: 'song', 
    image: 'impala.png',
    info: { year: '2019', genre: 'Psychedelic Pop', rating: 4, duration: '4:34' }
  },
  { 
    title: 'Let It Happen', 
    artist: 'Tame Impala', 
    type: 'song', 
    image: 'impala.png',
    info: { year: '2015', genre: 'Psychedelic Pop', rating: 5, duration: '7:47' }
  },
  { 
    title: 'Feels Like We Only Go Backwards', 
    artist: 'Tame Impala', 
    type: 'song', 
    image: 'impala.png',
    info: { year: '2012', genre: 'Psychedelic Pop', rating: 5, duration: '3:12' }
  },
  { 
    title: 'Mona Lisa', 
    artist: 'Dominic Fike', 
    type: 'song', 
    category: 'other', 
    image: 'lisa.png',
    info: { year: '2023', genre: 'Alternative R&B', rating: 4, duration: '3:06' }
  },
  { 
    title: 'Patience', 
    artist: 'Tame Impala', 
    type: 'song', 
    image: 'impala.png',
    info: { year: '2019', genre: 'Psychedelic Pop', rating: 4, duration: '4:52' }
  }
])

// Computed property for filtered items
const displayedItems = computed(() => {
  switch (selectedOption.value) {
    case 'tame-impala':
      return musicItems.filter(item => item.artist === 'Tame Impala')
    case 'albums':
      return musicItems.filter(item => item.type === 'album')
    case 'feats':
      return musicItems.filter(item => item.feat)
    case 'other':
      return musicItems.filter(item => item.category === 'other')
    default:
      return musicItems
  }
})
</script>