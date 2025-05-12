<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  import { writable } from 'svelte/store';

  let videos = [];
  let filteredVideos = writable([]);
  let categories = writable([]);
  let searchQuery = '';

  $: category = decodeURIComponent($page.params.category || 'all');

  // 🔁 Re-run filter when category changes
  $: $page.params.category, filterVideos();

  onMount(async () => {
    const response = await fetch('/full_translated.json');
    videos = await response.json();

    // Extract unique categories
    const uniqueCategories = [...new Set(videos.map(video => video.category.trim()))];
    categories.set(uniqueCategories);

    filterVideos(); // initial run
  });

  function filterVideos() {
    const query = searchQuery.toLowerCase();
    filteredVideos.set(
      videos.filter(video =>
        (category === 'all' || video.category.trim().toLowerCase() === category.trim().toLowerCase()) &&
        (video.title.toLowerCase().includes(query) || video.description.toLowerCase().includes(query))
      )
    );
  }

  function extractCleanTitle(rawTitle) {
    const parts = rawTitle.split(' - ').filter(Boolean);
    return parts.length >= 2 ? toTitleCase(parts[1]) : toTitleCase(rawTitle);
  }

  function toTitleCase(str) {
    return str
      .toLowerCase()
      .split(' ')
      .map(word => word.charAt(0).toUpperCase() + word.slice(1))
      .join(' ');
  }

  function extractKannadaTitle(rawKannada) {
  if (!rawKannada) return '';
  // Remove "ಕನ್ನಡ - " prefix and trailing " - [DATE] -"
  return rawKannada.replace(/^ಕನ್ನಡ\s*-\s*/, '').replace(/\s*-\s*\d{1,2}\s+\S+\s+\d{4}\s*-*$/, '').trim();
}

function formatDuration(duration) {
    const minMatch = duration.match(/(\d+)\s*MIN/i);
    const secMatch = duration.match(/(\d+)\s*SEC/i);

    const minutes = minMatch ? parseInt(minMatch[1]) : 0;
    const seconds = secMatch ? parseInt(secMatch[1]) : 0;

    const formatted = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    return `⏱️ ${formatted}`;
  }

</script>

<style>
  :global(body) {
    font-family: "Segoe UI", "Verdana", "Arial Rounded MT Bold", "Trebuchet MS", sans-serif;
    background-color: #f0f8ff;
    color: #333;
  }
</style>

<!-- Layout -->
<div class="px-4 md:px-6 flex flex-col md:flex-row gap-4 mx-auto max-w-7xl pt-5">
  <!-- Sidebar -->
  <aside class="hidden md:block md:w-1/4 bg-yellow-50 p-3 rounded-xl shadow self-start">
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
  </aside>

<!-- Main Content -->
<main class="w-full md:w-3/4 min-h-screen">
  <!-- Title + Search -->
  <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-3 mb-6">
    <!-- Category Title -->
    <div>
      {#if category.includes(' - ')}
        <h1 class="text-xl sm:text-2xl font-bold text-yellow-900 leading-tight">
          {category.split(' - ')[0]}<br />
          <span class="text-base sm:text-lg text-yellow-700">{category.split(' - ')[1]}</span>
        </h1>
      {:else}
        <h1 class="text-xl sm:text-2xl font-bold text-yellow-900">{category}</h1>
      {/if}
    </div>

    <!-- Search Bar -->
    <div class="w-full sm:w-auto">
      <input
        type="text"
        placeholder="🔍 {category}"
        class="w-full sm:w-[300px] px-4 py-3 text-xs border border-yellow-700 rounded-xl shadow focus:ring focus:ring-blue-300"
        bind:value={searchQuery}
        on:input={filterVideos}
      />
    </div>
  </div>

  <!-- Videos Grid -->
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
    <p class="text-center text-xl text-yellow-700 mt-16 font-bold animate-bounce">
      😢 No videos found in this category.
    </p>
  {/if}
</main>
</div>
