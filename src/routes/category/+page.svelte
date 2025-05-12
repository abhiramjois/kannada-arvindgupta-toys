<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';
  
    let categories = writable([]);
  
    onMount(async () => {
      const response = await fetch('/full_translated.json');
      const videos = await response.json();
      const uniqueCategories = [...new Set(videos.map(video => video.category.trim()))];
      categories.set(uniqueCategories);
    });
  </script>
  
  <div class="p-6 max-w-7xl md:mx-auto bg-yellow-50 rounded-xl m-2">
    <!-- <h1 class="text-2xl font-bold mb-6 text-blue-800">All Categories</h1> -->
  
    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-3 gap-4">
      {#each $categories as cat}
        <a
          href={`/category/${encodeURIComponent(cat)}`}
          class="block bg-yellow-200 text-yellow-900 font-medium rounded-xl py-4 px-4 shadow hover:bg-yellow-300 transition"
        >
        {#if cat.includes(' - ')}
        <span class="block">{cat.split(' - ')[0]}</span>
        <span class="block text-xs text-yellow-800 opacity-90">{cat.split(' - ')[1]}</span>
      {:else}
        {cat}
      {/if}
        </a>
      {/each}
    </div>
  </div>
  