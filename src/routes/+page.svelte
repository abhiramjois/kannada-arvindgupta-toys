<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  import { writable } from 'svelte/store';

  let videos = [];
  let filteredVideos = writable([]);
  let categories = writable([]);
  let searchQuery = '';

  $: category = decodeURIComponent($page.params.category || 'all');

  onMount(async () => {
    const response = await fetch('/full_translated.json');
    videos = await response.json();

    videos = shuffleArray(videos); // Randomize the videos

    const uniqueCategories = [...new Set(videos.map(video => video.category.trim()))];
    categories.set(uniqueCategories);

    filterVideos();
  });

  function filterVideos() {
    const query = searchQuery.toLowerCase();
    filteredVideos.set(
      videos.filter(video =>
        (category === 'all' || video.category.trim().toLowerCase() === category.trim().toLowerCase()) &&
        (
          (video.title && video.title.toLowerCase().includes(query)) ||
          (video.description && video.description.toLowerCase().includes(query)) ||
          (video.title_kn && video.title_kn.toLowerCase().includes(query))
        )
      )
    );
  }

  function shuffleArray(array) {
    return array.sort(() => Math.random() - 0.5);
  }

  function formatDuration(duration) {
    const minMatch = duration.match(/(\d+)\s*MIN/i);
    const secMatch = duration.match(/(\d+)\s*SEC/i);
    const minutes = minMatch ? parseInt(minMatch[1]) : 0;
    const seconds = secMatch ? parseInt(secMatch[1]) : 0;
    return `⏱️ ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
  }

  function extractCleanTitle(rawTitle) {
    const parts = rawTitle.split(' - ').filter(Boolean);
    return parts.length >= 2 ? toTitleCase(parts[1]) : toTitleCase(rawTitle);
  }

  function extractKannadaTitle(rawKannada) {
    if (!rawKannada) return '';
    return rawKannada.replace(/^ಕನ್ನಡ\s*-\s*/, '').replace(/\s*-\s*\d{1,2}\s+\S+\s+\d{4}\s*-*$/, '').trim();
  }

  function toTitleCase(str) {
    return str
      .toLowerCase()
      .split(' ')
      .map(word => word.charAt(0).toUpperCase() + word.slice(1))
      .join(' ');
  }
</script>

<style>
  :global(body) {
    font-family: "Segoe UI", "Verdana", "Arial Rounded MT Bold", "Trebuchet MS", sans-serif;
    background-color: #f0f8ff;
    color: #333;
  }
</style>

<div class="flex flex-col md:flex-row gap-4 items-start mx-auto max-w-7xl pt-5 px-4">
  <!-- Sidebar with Search + Categories (Sticky on small screens) -->
  <aside class="w-full md:w-1/4 md:top-5">
    <!-- Search bar: always visible -->
    <div class="md:mb-4 w-full">
      <input
        type="text"
        placeholder="🔍 Search for a material or a concept"
        class="w-full px-4 py-3 text-xs border border-orange-200 rounded-xl shadow focus:ring focus:ring-blue-300"
        bind:value={searchQuery}
        on:input={filterVideos}
      />
    </div>

    <!-- Categories: hidden on small screens -->
    <div class="bg-yellow-50 p-3 rounded-xl shadow w-full hidden md:block">
      <h2 class="text-base lg:text-lg font-bold mb-3 text-yellow-800">Categories</h2>
      <div class="flex flex-col gap-2">
        {#each $categories as cat}
          <a
            href={`/category/${encodeURIComponent(cat)}`}
            class="text-sm px-4 py-3 bg-yellow-200 text-yellow-900 font-medium hover:bg-yellow-300 transition text-left leading-tight rounded-md break-words"
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
  </aside>

  <!-- Video Grid -->
  <main class="w-full md:w-3/4 self-start">
    {#if $filteredVideos.length > 0}
      <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-2 xl:grid-cols-3">
        {#each $filteredVideos as video}
          <div class="bg-white rounded-xl shadow-md transition duration-300 hover:scale-[1.02] hover:shadow-xl flex flex-col h-full">
            <a href={`/${video.id}`} class="flex flex-col h-full">
              <!-- Image -->
              <div class="relative h-48 bg-gray-200 flex items-center justify-center overflow-hidden rounded-t-xl">
                <img
                  loading="lazy"
                  src={`/${video.thumbnail}`}
                  alt=""
                  class="w-full h-full object-cover transition-opacity duration-500 ease-in-out opacity-0"
                  on:load={(e) => e.target.classList.add('opacity-100')}
                />
              </div>

              <!-- Text content -->
              <div class="p-4 flex flex-col flex-grow">
                <div class="pb-4">
                  <h3 class="text-base sm:text-lg text-orange-700 font-semibold leading-tight">
                    {extractKannadaTitle(video.title_kn)}
                  </h3>
                  <p class="text-sm sm:text-base text-orange-700 leading-snug">
                    {extractCleanTitle(video.title)}
                  </p>
                </div>

                <!-- Spacer -->
                <div class="flex-grow"></div>

                <!-- Meta info -->
                <div class="text-sm text-gray-500 mt-2 flex items-center justify-between flex-wrap gap-2">
                  <span>{formatDuration(video.duration)}</span>
                  <span class="bg-yellow-200 text-yellow-900 font-medium text-xs px-3 py-1 rounded">
                    {video.category.split(' - ')[0]}
                  </span>
                </div>
              </div>
            </a>
          </div>
        {/each}
      </div>
    {:else}
      <p class="text-center text-xl text-yellow-900 mt-16 font-bold animate-bounce">
        Loading...
      </p>
    {/if}
  </main>
</div>
