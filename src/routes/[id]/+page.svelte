<script>
  import { page } from '$app/stores';
  import { onDestroy } from 'svelte';

  let video = null;
  let useYouTube = false;
  let relatedVideos = [];

  let unsubscribe;

  // Reactive when URL changes
  $: if ($page.params.id) {
    loadVideo($page.params.id);
  }

  async function loadVideo(id) {
    video = null;
    useYouTube = false;
    relatedVideos = [];

    const response = await fetch('/full_translated.json');
    const videos = await response.json();
    video = videos.find(v => v.id === id);

    if (video?.video_url) {
      try {
        const headResp = await fetch(video.video_url, { method: 'HEAD' });
        if (!headResp.ok) {
          useYouTube = true;
        }
      } catch (err) {
        useYouTube = true;
      }
    } else {
      useYouTube = true;
    }

    if (video) {
      relatedVideos = videos
        .filter(v => v.category === video.category && v.id !== video.id)
        .slice(0, 6);
    }
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
    return rawKannada
      .replace(/^ಕನ್ನಡ\s*-\s*/, '')
      .replace(/\s*-\s*\d{1,2}\s+\S+\s+\d{4}\s*-*$/, '')
      .trim();
  }
</script>

<div class="p-3 max-w-7xl mx-auto bg-white">
  <div class="flex flex-col lg:flex-row gap-4">
    <!-- Video Section -->
    <div class="lg:w-2/3 w-full">
      {#if video}
        <h1 class="text-xl font-bold text-gray-800 pt-5">
          {extractKannadaTitle(video.title_kn)} {extractCleanTitle(video.title)}
        </h1>

        {#if useYouTube}
          <div class="aspect-w-16 aspect-h-9 mt-4">
            <iframe
              class="w-full h-96 rounded"
              src={`https://www.youtube.com/embed/${video.id}`}
              frameborder="0"
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen
            ></iframe>
          </div>
        {:else}
          <div class="bg-black rounded mt-4">
            <video controls class="w-full max-h-[60vh] rounded">
              <source src={video.video_url} type="video/mp4" />
              Your browser does not support the video tag.
            </video>
          </div>
        {/if}

        <!-- Description Section -->
        <div class="mt-4 p-4 bg-gray-100 rounded-xl">
          <p class="text-gray-800">{video.description_kn}</p>
          <p class="mt-4 text-gray-800">{video.description}</p>
        </div>
      {:else}
        <p>Loading...</p>
      {/if}
    </div>

    <!-- Related Videos Section -->
    <div class="lg:ml-3 bg-white rounded-lg w-full lg:w-1/3">
      <h2 class="text-xl font-semibold">Related Videos</h2>
      <ul class="mt-4">
        {#each relatedVideos as relatedVideo}
          <li class="mb-4">
            <div class="bg-white rounded-lg flex gap-2 lg:gap-2 items-start">
              <img
                src={relatedVideo.thumbnail}
                alt={relatedVideo.title}
                class="w-32 h-auto object-contain rounded"
              />
              <div class="flex-1 pl-2">
                <a href={`/${relatedVideo.id}`} class="text-blue-500 hover:underline font-bold">
                  {relatedVideo.title_kn
                    ? extractKannadaTitle(relatedVideo.title_kn)
                    : extractCleanTitle(relatedVideo.title)}
                </a>
                <p class="text-sm text-gray-500 mt-1">{extractCleanTitle(relatedVideo.title)}</p>
                <p class="text-sm text-gray-500 mt-1">{relatedVideo.duration}</p>
              </div>
            </div>
          </li>
        {/each}
      </ul>
    </div>
  </div>
</div>
