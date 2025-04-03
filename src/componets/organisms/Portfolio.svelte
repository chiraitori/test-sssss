<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  const projects = [
    {
      title: "Game Project 1",
      description: "A 3D adventure game built with Unity",
      tags: ["Unity", "C#", "3D Modeling"],
      image: "/images/project1.jpg" // Replace with actual image path
    },
    {
      title: "Interactive Web Experience",
      description: "A WebGL-based interactive story",
      tags: ["JavaScript", "Three.js", "WebGL"],
      image: "/images/project2.jpg" // Replace with actual image path
    },
    {
      title: "Mobile RPG Game",
      description: "Fantasy role-playing game for iOS and Android",
      tags: ["Unity", "Mobile", "Game Design"],
      image: "/images/project3.jpg" // Replace with actual image path
    },
    {
      title: "Streaming Overlay Pack",
      description: "Custom animated overlays for streamers",
      tags: ["After Effects", "Animation", "Streaming"],
      image: "/images/project4.jpg" // Replace with actual image path
    }
  ];
  
  let visibleProjects = [];
  
  function handleIntersection(entries) {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const index = parseInt(entry.target.dataset.index);
        if (!visibleProjects.includes(index)) {
          visibleProjects = [...visibleProjects, index];
        }
      }
    });
  }
  
  onMount(() => {
    const observer = new IntersectionObserver(handleIntersection, {
      root: null,
      rootMargin: '0px',
      threshold: 0.1
    });
    
    document.querySelectorAll('.project-card').forEach(card => {
      observer.observe(card);
    });
    
    return () => {
      observer.disconnect();
    };
  });
</script>

<section id="portfolio" class="py-24 bg-gray-900">
  <div class="container mx-auto px-6">
    <h2 class="text-4xl font-bold text-center mb-16 text-white">My <span class="text-blue-500">Portfolio</span></h2>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 gap-8">
      {#each projects as project, i}
        <div class="project-card" data-index={i}>
          {#if visibleProjects.includes(i)}
            <div 
              in:fly={{ y: 50, duration: 800, delay: i * 200 }}
              class="bg-gray-800 rounded-xl overflow-hidden shadow-lg hover:shadow-blue-500/20 hover:translate-y-[-5px] transition-all duration-300"
            >
              <div class="h-64 overflow-hidden">
                <div class="w-full h-full bg-gradient-to-br from-blue-500/70 to-purple-600/70 flex items-center justify-center text-xl font-bold text-white">
                  {project.title} Preview
                </div>
              </div>
              
              <div class="p-6">
                <h3 class="text-xl font-bold mb-2 text-white">{project.title}</h3>
                <p class="text-gray-400 mb-4">{project.description}</p>
                
                <div class="flex flex-wrap gap-2 mb-6">
                  {#each project.tags as tag}
                    <span class="px-3 py-1 bg-blue-900/50 text-blue-300 text-xs font-medium rounded-full">{tag}</span>
                  {/each}
                </div>
                
                <div class="flex justify-between items-center">
                  <a href="#" class="text-blue-400 hover:text-blue-300 font-medium flex items-center gap-1 group">
                    <span>View details</span>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 transform group-hover:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                    </svg>
                  </a>
                </div>
              </div>
            </div>
          {/if}
        </div>
      {/each}
    </div>
  </div>
</section>
