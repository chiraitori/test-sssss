<script>
  import QRDonationCard from '../molecules/QRDonationCard.svelte';
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';
  
  let visible = false;
  
  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      });
    }, { threshold: 0.1 });
    
    observer.observe(document.querySelector('#donate'));
    
    return () => {
      observer.disconnect();
    };
  });
</script>

<section id="donate" class="py-24 bg-gradient-to-b from-gray-900 to-gray-800">
  <div class="container mx-auto px-6">
    <h2 class="text-4xl font-bold text-center mb-4 text-white">Support My <span class="text-blue-500">Work</span></h2>
    <p class="text-gray-400 max-w-2xl mx-auto text-center mb-16">Your support helps me create better content and games. Every donation is appreciated and helps fuel my creativity.</p>
    
    {#if visible}
      <div in:fade={{ duration: 800 }} class="flex flex-col lg:flex-row items-center justify-center gap-16">
        <div class="w-full max-w-md">
          <QRDonationCard 
            playerDuoLink="https://playerduo.com/yourusername" 
            donationTitle="Support My Stream" 
            description="Scan to donate and get special perks on my streams!"
          />
        </div>
        
        <div class="w-full max-w-lg">
          <div class="bg-gray-800 rounded-xl p-8 shadow-lg">
            <h3 class="text-2xl font-bold mb-6 text-white">Why Support?</h3>
            
            <div class="space-y-6">
              <div class="flex items-start gap-4">
                <div class="bg-blue-600 p-3 rounded-lg">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-semibold text-white">Exclusive Content</h4>
                  <p class="text-gray-400">Get access to behind-the-scenes content and development updates</p>
                </div>
              </div>
              
              <div class="flex items-start gap-4">
                <div class="bg-blue-600 p-3 rounded-lg">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-semibold text-white">Early Access</h4>
                  <p class="text-gray-400">Be the first to play new games and demos before public release</p>
                </div>
              </div>
              
              <div class="flex items-start gap-4">
                <div class="bg-blue-600 p-3 rounded-lg">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                <div>
                  <h4 class="text-lg font-semibold text-white">Special Mention</h4>
                  <p class="text-gray-400">Get your name in the credits of my projects and streams</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    {/if}
  </div>
</section>
