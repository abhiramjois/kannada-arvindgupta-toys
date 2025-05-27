<script>
  // No interactivity needed for now
  // Could add mobile menu toggle, image lazy loading, etc.
</script>

<main class="max-w-5xl mx-auto py-3 px-4 sm:py-5 text-gray-800 min-h-screen">
  <!-- Hero Section -->
  <section class="mb-4 sm:mb-6">
    <div class="flex flex-col lg:flex-row gap-4 lg:gap-6">
      <img 
        src="children-engaging.jpg" 
        alt="Children engaging with educational materials" 
        class="w-full lg:w-2/5 h-fit my-auto rounded-lg shadow-sm"
      >
      <div class="w-full lg:w-3/5 bg-white p-4 sm:p-5 border-red-300 border rounded-lg flex flex-col gap-3 shadow-sm">
        <p class="leading-relaxed text-sm sm:text-base mb-4">
          This project is an <strong>offline first, bilingual interface</strong> for the Arvind Gupta Toy repository in Kannada. The main intent is to make the repository accessible to communities that are often excluded digitally. This effort is part of the sanchari.local, a travelling library. Sanchari.local was conceptualized under <strong>Samagra Arogya</strong>, a long-term community-based research initiative by <strong>Aruvu Collaboratory</strong> and <strong>KHPT</strong>, working with seven <strong>Gram Panchayats in Kundapura</strong> to understand social determinants of health in a place based manner.
        </p>
        <a 
          href="https://github.com/abhiramjois/kannada-arvindgupta-toys/" 
          class="hover:bg-red-500 active:bg-red-600 p-3 sm:p-4 hover:text-white font-bold rounded bg-white text-red-500 border-2 border-red-500 w-full text-center text-sm sm:text-base transition-colors duration-200 touch-manipulation"
          target="_blank"
          rel="noopener noreferrer"
        >
          Link to project Github
        </a>
      </div>
    </div>
  </section>

  <!-- Features Section -->
  <section class="mb-4 sm:mb-6">
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
      <!-- Kannada metadata -->
      <div class="bg-white p-4 sm:p-6 rounded-lg text-center text-red-700 border border-red-500 border-dashed shadow-sm">
        <div class="w-12 h-12 sm:w-16 sm:h-16 mx-auto mb-3 sm:mb-4 relative flex items-center justify-center">
          <div class="text-5xl sm:text-7xl text-red-500">ಕ</div>
        </div>
        <h3 class="font-bold text-base sm:text-lg mb-2">Kannada metadata</h3>
        <p class="text-xs sm:text-sm">Translated video titles, descriptions and categories to Kannada and implemented a bilingual interface with a basic search feature</p>
      </div>
      
      <!-- Offline first -->
      <div class="bg-white p-4 sm:p-6 rounded-lg text-center text-red-700 border border-red-500 border-dashed shadow-sm">
        <div class="w-12 h-12 sm:w-16 sm:h-16 mx-auto mb-3 sm:mb-4 relative">
          <svg class="w-12 h-12 sm:w-16 sm:h-16 mx-auto text-red-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M2 20h.01" />
            <path d="M7 20v-4" />
            <path d="M12 20v-8" />
            <path d="M17 20V8" />
            <path d="M22 20V4" />
          </svg>
        </div>
        <h3 class="font-bold text-base sm:text-lg mb-2">Offline first</h3>
        <p class="text-xs sm:text-sm">This website was made to be self hosted on any server including a raspberry PI to enable fully offline use. Designed to be part of offline mesh networks</p>
      </div>

      <!-- Community-Focused -->
      <div class="bg-white p-4 sm:p-6 rounded-lg text-center text-red-700 border border-red-500 border-dashed shadow-sm sm:col-span-2 lg:col-span-1">
        <div class="w-12 h-12 sm:w-16 sm:h-16 mx-auto mb-3 sm:mb-4 relative">
          <div class="absolute top-1 left-1 sm:top-2 sm:left-2 w-3 h-3 sm:w-4 sm:h-4 border-2 sm:border-4 border-red-500 rounded-full"></div>
          <div class="absolute top-1 right-1 sm:top-2 sm:right-2 w-3 h-3 sm:w-4 sm:h-4 border-2 sm:border-4 border-red-500 rounded-full"></div>
          <div class="absolute bottom-1 left-1 sm:bottom-2 sm:left-2 w-3 h-3 sm:w-4 sm:h-4 border-2 sm:border-4 border-red-500 rounded-full"></div>
          <div class="absolute bottom-1 right-1 sm:bottom-2 sm:right-2 w-3 h-3 sm:w-4 sm:h-4 border-2 sm:border-4 border-red-500 rounded-full"></div>
          <div class="absolute top-3 left-3 right-3 bottom-3 sm:top-4 sm:left-4 sm:right-4 sm:bottom-4 border-2 border-red-500 rounded-full"></div>
        </div>
        <h3 class="font-bold text-base sm:text-lg mb-2">For Community Engagement</h3>
        <p class="text-xs sm:text-sm">Designed as part of Sanchari.local, a traveling library that is part of an ongoing community engagement Samagra Arogya to understand access to education as a social determinant of health</p>
      </div>
    </div>
  </section>

  <!-- About Arvind Gupta Toys Section -->
  <section class="mb-4 sm:mb-6">
    <div class="flex flex-col lg:flex-row gap-4">
      <div class="w-full lg:w-3/5">
        <div class="bg-white border-red-300 p-4 sm:p-5 border rounded-lg mb-4 shadow-sm">
          <h2 class="text-lg sm:text-xl font-semibold mb-2">About Arvind Gupta Toys</h2>
          <p class="text-sm sm:text-base leading-relaxed">
            Arvind Gupta Toys is a remarkable collection of over 8,000 videos that demonstrate how to create toys and experiments explaining basic science and mathematics concepts using everyday items—often materials that might otherwise be discarded as trash. Although the repository exists on YouTube and arvindguptatoys.com, it lacks proper organization and searchability, making it difficult for educators and learners to navigate effectively.
          </p>
        </div>
        <p class="text-sm sm:text-base leading-relaxed bg-red-100 text-red-900 p-4 rounded-lg">
          Mr. Arvind Gupta has made his work available under Creative Commons licensing, opening the door for projects like this one to exist and make his educational content more accessible to communities that are often excluded digitally.
        </p>
      </div>
      <div class="w-full lg:w-2/5 flex flex-col gap-4 my-auto">
        <img src="arvind_g.webp" alt="Arvind Gupta" class="w-full h-auto rounded-lg shadow-sm">
        <div class="flex flex-col sm:flex-row gap-2 sm:gap-4 w-full">
          <a 
            href="https://www.youtube.com/@arvindguptatoys" 
            class="hover:bg-red-500 active:bg-red-600 p-3 sm:p-4 hover:text-white font-bold rounded bg-white text-red-500 border-2 border-red-500 w-full text-center text-sm sm:text-base transition-colors duration-200 touch-manipulation"
            target="_blank"
            rel="noopener noreferrer"
          >
            Youtube link
          </a>
          <a 
            href="https://www.arvindguptatoys.com/" 
            class="hover:bg-red-500 active:bg-red-600 p-3 sm:p-4 hover:text-white font-bold rounded bg-white text-red-500 border-2 border-red-500 w-full text-center text-sm sm:text-base transition-colors duration-200 touch-manipulation"
            target="_blank"
            rel="noopener noreferrer"
          >
            Website link
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- Community mesh network Section -->
  <section class="mb-4 sm:mb-6">
    <div class="flex flex-col lg:flex-row gap-4 lg:gap-6">
      <div class="w-full lg:w-1/2 flex flex-col gap-4">
        <img src="mesh.jpg" alt="Mesh network setup" class="w-full h-auto rounded-lg shadow-sm">
        <img src="sanchari.jpg" alt="Sanchari local library" class="w-full h-auto rounded-lg shadow-sm">
        <img src="sanchari-ss.png" alt="Sanchari screenshot" class="w-full h-auto rounded-lg shadow-sm">
      </div>
      <div class="w-full lg:w-1/2 bg-white border border-red-300 p-4 sm:p-5 rounded-lg shadow-sm">
        <h2 class="text-lg sm:text-xl font-semibold my-2 sm:my-4">Community mesh network in Hara</h2>
        <p class="text-sm sm:text-base leading-relaxed mb-4">
          Our work in Samagra Arogya spans seven Gram Panchayats, focusing on shifting governance from welfare models to care-based infrastructures. Through this lens, we've identified "access to education" and "the right to communicate" as primary determinants of health, particularly in remote tribal communities.
        </p>
        <p class="text-sm sm:text-base leading-relaxed mb-4">
          We have been working in Hara, a tribal hamlet in Kundapura to build a community mesh network. The cellular network and internet coverage in the area is very poor and hence we wanted to experiment with co imagining possibilities of a local area MESH and an offline internet before we figured out the logistics of getting an internet fiber line in the place.
        </p>
        <div class="flex flex-col gap-4 sm:gap-5">
          <div>
            <h3 class="text-lg sm:text-xl font-medium mb-2">Sanchari.local - A traveling library</h3>
            <p class="text-sm sm:text-base leading-relaxed mb-4">
              The <span class="font-medium">sanchari.local</span> emerged from our community engagement in Hara as a Raspberry Pi device hosting multiple offline repositories, information, and libraries and a hotspot. Devices in the vicinity can connect to this hotspot and access services on it. Or access it on the larger offline mesh network. The vision goes beyond simply providing access to existing content, the idea is to enable communities to create and contribute their own repositories with their local knowledge systems made of images, videos, maps, websites, and local knowledge.
            </p>
            <p class="text-sm sm:text-base leading-relaxed">
              The current version of sanchari.local contains the Arving Gupta toy repository, "Stories from Hara"—an offline story map in English and Kannada, Jellyfin Media Server for streaming local content and a library of Pratham books.
            </p>
          </div>
          <a 
            href="https://untold.town/magazine/2025/01/sanchari-local-in-hara-early-explorations-of-a-traveling-raspberry-pi-library/" 
            class="hover:bg-red-500 active:bg-red-600 p-3 sm:p-4 hover:text-white font-bold rounded bg-white text-red-500 border-2 border-red-500 w-full text-center text-sm sm:text-base transition-colors duration-200 touch-manipulation"
            target="_blank"
            rel="noopener noreferrer"
          >
            Read more about sanchari.local
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- Personal Anecdote Section -->
  <section class="mb-4 sm:mb-6 bg-white border border-red-300 p-4 sm:p-5 rounded-lg shadow-sm">
    <div class="flex flex-col lg:flex-row gap-4">
      <div class="w-full lg:w-1/5">
        <h2 class="text-lg sm:text-2xl font-semibold mb-2">A Personal Anecdote</h2>
      </div>
      <div class="w-full lg:w-4/5">
        <p class="text-sm sm:text-base leading-relaxed mb-4">
          This website is a manifestation of the curiosity and experimentation that AGT videos on Youtube sparked in me when I was a child. I remember I had gone to my childhood friend Kaushik's house and he showed me a rat that he had made from a coconut. I was extremely fascinated by it and asked him where he learnt how to do that, he then showed me arvindguptatoys.com.
        </p>
        <p class="text-sm sm:text-base leading-relaxed mb-4">
          Growing up with internet access in the early 2010s meant that I was always in the hunt for fun, exciting websites. The use of internet by children was not a common phenomenon back then, this was a layer beneath the fact that there was not a lot of internet representation and media from the Indian subcontinent. In a time like this finding this curated effort from the sub continent dedicated to children like me was a huge find. It also greatly influenced my perceptions of science and what it does.
        </p>
        <p class="text-sm sm:text-base leading-relaxed mb-4">
          The philosophy and the playfulness of scientific enquiry was somewhat internalised in me and shaped a major part of how I viewed science and its role in a society. Life happened and I grew up, forgot about the repository until I started working on the sanchari.local in Hara at the Aruvu Collaboratory.
        </p>
      </div>
    </div>
  </section>

  <!-- Going Forward Section -->
  <section class="bg-white border border-red-300 p-4 sm:p-5 rounded-lg shadow-sm mb-4 sm:mb-6">
    <div class="flex flex-col lg:flex-row gap-4">
      <h2 class="text-lg sm:text-2xl font-semibold mb-2 w-full lg:w-1/5">Going Forward</h2>
      <div class="w-full lg:w-4/5">
        <p class="text-sm sm:text-base leading-relaxed mb-4">
          This Kannada repository of Arvind Gupta Toys represents just the beginning. Future plans include expanding to the complete multilingual collection and implementing NLP-based tagging to categorize videos by materials used and concepts explained, making the database more comprehensive and the interface more intuitive.
        </p>
        <p class="text-sm sm:text-base leading-relaxed">
          Each video in this collection carries the potential to spark the same wonder and curiosity that shaped my own understanding of science. By making this content accessible offline and in local languages, we hope to ensure that geographic and digital barriers don't prevent the next generation of young scientists, inventors, and dreamers from discovering the joy of learning through play.
        </p>
      </div>
    </div>
  </section>

  <!-- Quote Section -->
  <blockquote class="italic text-gray-600 mt-4 sm:mt-6 max-w-2xl font-bold text-center p-4 sm:p-5 mx-auto text-sm sm:text-base">
    "And somewhere there are engineers helping others fly faster than sound. But, where are the engineers helping those who must live on the ground?" — Young Oxfam Poster
  </blockquote>
</main>

<style>
  /* Custom styles for better mobile experience */
  @media (max-width: 640px) {
    /* Ensure touch targets are at least 44px */
    .touch-manipulation {
      min-height: 44px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    /* Improve text readability on mobile */
    p {
      line-height: 1.6;
    }
    
    /* Better spacing for mobile */
    section {
      margin-bottom: 1rem;
    }
  }
  
  /* Smooth scrolling for anchor links */
  html {
    scroll-behavior: smooth;
  }
  
  /* Focus styles for keyboard navigation */
  a:focus {
    outline: 2px solid #ef4444;
    outline-offset: 2px;
  }
</style>