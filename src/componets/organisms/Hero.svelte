<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let visible = false;
  
  onMount(() => {
    visible = true;
  });
</script>

<section class="relative min-h-screen bg-gradient-to-b from-gray-900 to-gray-800 text-white flex items-center">
  <div class="absolute inset-0 overflow-hidden">
    <div class="absolute inset-0 bg-[radial-gradient(circle_at_30%_30%,rgba(59,130,246,0.2),transparent_70%)]"></div>
  </div>
  
  <div class="container mx-auto px-6 z-10">
    <div class="flex flex-col md:flex-row items-center justify-between gap-12">
      <div class="w-full md:w-1/2">
        {#if visible}
          <div in:fly={{ y: 50, duration: 1000, delay: 200 }}>
            <h1 class="text-4xl sm:text-5xl lg:text-6xl font-bold mb-6 bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-purple-500">
              Game Developer & Streamer
            </h1>
          </div>
          
          <div in:fade={{ duration: 1000, delay: 500 }}>
            <p class="text-xl text-gray-300 mb-8">Creating engaging experiences through code and content. Support my journey through PlayerDuo.</p>
            
            <div class="flex flex-wrap gap-4">
              <a href="#portfolio" class="px-8 py-3 bg-blue-600 hover:bg-blue-700 rounded-lg font-medium transition-colors duration-300">
                My Work
              </a>
              <a href="#donate" class="px-8 py-3 bg-transparent border border-blue-400 hover:bg-blue-400/10 rounded-lg font-medium transition-colors duration-300">
                Support Me
              </a>
            </div>
          </div>
        {/if}
      </div>
      
      <div class="w-full md:w-1/2">
        {#if visible}
          <div class="relative" in:fly={{ y: 50, duration: 1000, delay: 600 }}>
            <div class="w-full h-80 sm:h-96 md:h-[28rem] rounded-2xl overflow-hidden shadow-xl shadow-blue-500/20 relative">
              <!-- Replace with actual profile image -->
              <div class="absolute inset-0 bg-gradient-to-br from-purple-600 to-blue-500 flex items-center justify-center text-4xl font-bold">
                Your Image
              </div>
            </div>
            
            <div class="absolute -bottom-4 -right-4 w-24 h-24 bg-blue-600 rounded-lg flex items-center justify-center transform rotate-6 animate-pulse">
              <span class="text-xl font-bold">Live</span>
            </div>
          </div>
        {/if}
      </div>
    </div>
  </div>
</section>
