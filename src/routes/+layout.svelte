<script>
  import '../app.css';
  let { children } = $props();
</script>

<style>
  .background-grid {
    background-color: #ffffff; /* soft paper-like tone */
    background-image: 
      linear-gradient(to right, #f0f0f0 1px, transparent 1px),
      linear-gradient(to bottom, #f0f0f0 1px, transparent 1px);
    background-size: 20px 20px; /* grid size */
    background-repeat: repeat;
  }

  /* Sticky navbar for small screens */
  .sticky-navbar {
    position: sticky;
    top: 0;
    z-index: 10; /* Ensure it stays on top */
    background-color: #ffffff; /* Optional: ensure the background stays opaque when sticky */
    /* border-bottom: 1px solid #0b0b0b;  */
  }
</style>

<div class="min-h-screen flex flex-col text-pink-700 background-grid">
  <!-- Layout container -->
  <div class="max-w-7xl mx-auto w-full md:px-6 flex flex-col flex-grow">

    <!-- Navbar -->
    <header class="sticky-navbar border border-dotted border-orange-600 md:bg-transparent text-orange-700 p-4 md:mt-4 rounded shadow-sm">
      <div class=" flex flex-col items-center md:flex-row md:justify-between md:items-center md:text-left gap-4">
        
        <!-- Combined Kannada + English Title -->
        <a href="/" class="flex items-center gap-4 md:text-left hover:underline">
          <img src="/logo.png" alt="Logo" class=" h-12 w-12 object-contain" />
          <div class="flex flex-col leading-tight">
            <span class="text-2xl sm:text-3xl font-bold">ಎಜಿಟಿ ಆರ್ಕೈವ್ಸ್</span>
            <span class="text-lg sm:text-xl font-medium font-mono text-orange-600">AGT Archives</span>
          </div>
        </a>        
    
        <!-- Nav Buttons -->
        <nav class="flex gap-3 text-sm">
          <a href="/category" class="bg-white px-4 py-2 border border-gray-400 rounded hover:bg-gray-100 transition">
            Categories
          </a>
          <a href="/about" class="bg-white px-4 py-2 border border-gray-400 rounded hover:bg-gray-100 transition">
            About
          </a>
        </nav>
      </div>
    </header>    

    <!-- Main Content -->
    <main class="flex-grow">
      {@render children()}
    </main>

    <!-- Footer -->
    <footer class="bg-gray-100 bg-opacity-80 text-sm text-gray-600 py-4 text-center rounded-t">
      {new Date().getFullYear()}, AGT Archives. This project builds upon Arvind Gupta's Creative Commons licensed content. Please respect the original licensing terms when using or redistributing this software.
    </footer>
  </div>
</div>
