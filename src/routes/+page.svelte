<script>
    import Hero from '../componets/organisms/Hero.svelte';
    import Portfolio from '../componets/organisms/Portfolio.svelte';
    import DonationSection from '../componets/organisms/DonationSection.svelte';
    import { onMount, onDestroy } from 'svelte';
    
    let isLoading = true;
    let loadingTimer;
    let maxLoadingTimer;
    
    onMount(() => {
      // Shorter loading time (300ms instead of 1000ms)
      loadingTimer = setTimeout(() => {
        isLoading = false;
      }, 300);
      
      // Failsafe - maximum loading time of 3 seconds
      maxLoadingTimer = setTimeout(() => {
        if (isLoading) {
          console.log('Force stopping the loader after timeout');
          isLoading = false;
        }
      }, 3000);
    });
    
    onDestroy(() => {
      // Clean up timers to avoid memory leaks
      if (loadingTimer) clearTimeout(loadingTimer);
      if (maxLoadingTimer) clearTimeout(maxLoadingTimer);
    });
</script>
  
<svelte:head>
  <title>My Portfolio | Game Developer & Streamer</title>
</svelte:head>
  
{#if isLoading}
  <div class="fixed inset-0 bg-gray-900 flex items-center justify-center z-50">
    <div class="w-16 h-16 border-4 border-t-blue-500 border-r-transparent border-b-blue-500 border-l-transparent rounded-full animate-spin"></div>
  </div>
{:else}
  <main class="bg-gray-900 text-white">
    <Hero />
    <Portfolio />
    <DonationSection />
    
    <footer class="bg-gray-900 border-t border-gray-800 py-12">
      <div class="container mx-auto px-6">
        <div class="flex flex-col md:flex-row justify-between items-center gap-6">
          <div>
            <h2 class="text-2xl font-bold">John Doe</h2>
            <p class="text-gray-400">Game Developer & Content Creator</p>
          </div>
          
          <div class="flex gap-4">
            <a href="https://youtube.com" target="_blank" rel="noopener noreferrer" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-red-600 transition-colors">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/>
              </svg>
            </a>
            <a href="https://twitter.com" target="_blank" rel="noopener noreferrer" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-blue-400 transition-colors">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"/>
              </svg>
            </a>
            <a href="https://github.com" target="_blank" rel="noopener noreferrer" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-gray-600 transition-colors">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
              </svg>
            </a>
            <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-blue-700 transition-colors">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667h-3.554v-11.452h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zm-15.11-13.019c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019h-3.564v-11.452h3.564v11.452z"/>
              </svg>
            </a>
          </div>
        </div>
        
        <div class="mt-8 pt-8 border-t border-gray-800 text-center text-gray-500 text-sm">
          <p>&copy; {new Date().getFullYear()} John Doe. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </main>
{/if}
  
<style>
  :global(html, body) {
    background-color: #111827;
    scroll-behavior: smooth;
  }
</style>
