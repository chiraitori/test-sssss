<script>
  import { onMount } from 'svelte';
  import QRCode from 'qrcode';
  
  export let playerDuoLink = "https://playerduo.com/yourusername";
  export let donationTitle = "Support My Content";
  export let description = "Scan to donate through PlayerDuo";
  
  let qrCanvas;
  
  onMount(() => {
    if (qrCanvas) {
      QRCode.toCanvas(qrCanvas, playerDuoLink, {
        width: 180,
        margin: 1,
        color: {
          dark: '#0f172a',
          light: '#ffffff'
        }
      });
    }
    
    const card = document.querySelector('.qr-card');
    card.addEventListener('mousemove', (e) => {
      const rect = card.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      
      const centerX = rect.width / 2;
      const centerY = rect.height / 2;
      
      const angleX = (y - centerY) / 20;
      const angleY = (centerX - x) / 20;
      
      card.style.transform = `perspective(1000px) rotateX(${angleX}deg) rotateY(${angleY}deg)`;
    });
    
    card.addEventListener('mouseleave', () => {
      card.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
    });
  });
</script>

<div class="qr-card bg-white rounded-2xl shadow-xl overflow-hidden transition-all duration-300 hover:shadow-2xl hover:shadow-blue-500/20 w-full max-w-xs mx-auto" style="transform-style: preserve-3d;">
  <div class="p-6 bg-gradient-to-br from-blue-600 to-purple-600 text-white">
    <h3 class="text-xl font-bold mb-2">{donationTitle}</h3>
    <p class="text-blue-100">{description}</p>
  </div>
  
  <div class="p-6 flex flex-col items-center justify-center bg-white">
    <div class="mb-4 p-2 bg-white rounded-lg shadow-inner w-48 h-48 flex items-center justify-center">
      <canvas bind:this={qrCanvas} width="180" height="180"></canvas>
    </div>
    
    <div class="text-center">
      <p class="text-gray-600 text-sm mb-3">Or click the button below</p>
      <a 
        href={playerDuoLink} 
        target="_blank"
        rel="noopener noreferrer" 
        class="inline-flex items-center justify-center px-6 py-2.5 bg-blue-600 text-white font-medium rounded-lg hover:bg-blue-700 transition-colors group"
      >
        <span>Donate on PlayerDuo</span>
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-2 transform group-hover:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
        </svg>
      </a>
    </div>
  </div>
</div>
