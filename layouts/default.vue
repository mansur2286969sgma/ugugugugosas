<template>
  <div class="min-h-screen flex flex-col bg-gray-900">
    <header class="flex w-full items-center justify-between bg-black shadow-sm py-2 sticky top-0 z-50 text-white">
      <div class="basis-1/4 items-center justify-start px-10">
        <img src="/assets/images/water.png" alt="Logo" class="h-12 w-12">
      </div>
      <div class="basis-1/4"></div>
      <nav class="basis-1/2 flex flex-row items-center justify-end px-4 gap-4">
        <NuxtLink to="/" class="my-auto p-2 hover:bg-white text-[#00CCFF]">Home</NuxtLink>
        <NuxtLink to="/Content" class="my-auto p-2 hover:bg-white text-[#00CCFF]">Content</NuxtLink>
        <NuxtLink to="/login" class="my-auto p-2 hover:bg-white text-[#00CCFF]">Login</NuxtLink>
        <NuxtLink to="/logout" class="my-auto p-2 hover:bg-white text-[#00CCFF]">LogOut</NuxtLink>
      </nav>
    </header>

    <main class="flex-1">
      <slot /> 
    </main>

    <footer class="w-full bg-black border-t-2 border-[#00CCFF]">
      <div class="flex items-center justify-center px-4 py-2 gap-4">
        <a href="https://www.youtube.com/"> <img src="/assets/images/youtube.png" class="w-16 h-16"> </a>
        <a href="https://www.youtube.com/"> <img src="/assets/images/youtube.png" class="w-16 h-16"> </a>
        <a href="https://www.youtube.com/"> <img src="/assets/images/youtube.png" class="w-16 h-16"> </a>
      </div>
      <div class="w-full bg-gray-900 border-t-2 border-[#00CCFF]"> <div class="text-xs text-gray-500 text-center">
          <p>2025 Mansur corp.</p>
          <p>All rights reserved</p> </div>
      </div>
    </footer>
  </div>
</template>


