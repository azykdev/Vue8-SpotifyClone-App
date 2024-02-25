<template>
  <audio
    src="https://filesamples.com/samples/audio/mp3/sample3.mp3"
    ref="audioPlayer"
    preload="auto"
  ></audio>
  <div class="flex" style="height: 88vh">
    <!-- sidebar -->
    <div class="h-full w-56 bg-black flex-none relative">
      <div class="p-6">
        <img
          src="https://storage.googleapis.com/pr-newsroom-wp/1/2018/11/Spotify_Logo_CMYK_Green.png"
          class="h-10"
        />
      </div>
      <div class="mx-2 mb-5">
        <button
          @click="setId = page.id"
          v-for="page in pages"
          :class="`w-full rounded px-3 py-2 flex items-center justify-start font-semibold text-sm ${
            setId === page.id ? ' bg-gray-700 text-white' : ' text-gray-300'
          } `"
        >
          <i :class="`${page.icon}`" class="mr-3"></i>
          <p>{{ page.name }}</p>
        </button>
      </div>
      <div class="mx-5">
        <h1 class="mb-3 text-xs text-slate-100 uppercase tracking-widest">
          playlists
        </h1>
        <button
          class="mb-3 flex justify-start items-center opacity-75 hover:opacity-100 transition-opacity"
        >
          <img
            src="https://cdn2.iconfinder.com/data/icons/ios-7-icons/50/plus-512.png"
            alt=""
            class="bg-white w-8 h-8 mr-3 rounded"
          />
          <p class="text-sm text-white font-semibold">Create Playlist</p>
        </button>
        <button
          class="mb-3 flex justify-start items-center opacity-75 hover:opacity-100 transition-opacity"
        >
          <img
            src="https://www.clipartmax.com/png/middle/58-587249_small-heart-icon-vector-instagram-like-icon-png.png"
            alt=""
            class="bg-white w-8 h-8 mr-3 rounded p-1"
          />
          <p class="text-sm text-white font-semibold">Liked Songs</p>
        </button>
        <div class="w-full h-px my-3 bg-slate-200"></div>
      </div>
      <div class="mx-5">
        <div class="w-full h-8 overflow-y-scroll my-4">
          <p
            v-for="album in albums"
            class="text-slate-300 hover:text-white text-sm py-1"
          >
            {{ album.name }}
          </p>
        </div>
        <button
          class="text-sm flex items-center justify-start text-slate-300 hover:text-white"
        >
          <i class="fa-regular fa-circle-down mr-3"></i>
          <p>Install App</p>
        </button>
      </div>
      <div class="absolute bottom-0">
        <img src="https://source.unsplash.com/random/500×500/?music" alt="" />
      </div>
    </div>
    <!-- main content -->
    <div class="w-full h-full relative overflow-y-scroll">
      <!-- header -->
      <div
        class="w-full sticky top-0 p-5 flex items-center justify-between bg-zinc-900"
      >
        <div class="flex items-center">
          <button
            class="rounded-full mr-3 w-8 h-8 bg-black font-thin text-white"
          >
            <i class="fa-solid fa-angle-left text-2xl"></i>
          </button>
          <button class="rounded-full w-8 h-8 bg-black font-thin text-white">
            <i class="fa-solid fa-angle-right text-2xl"></i>
          </button>
        </div>
        <div class="relative">
          <button
            class="py-1 px-2 bg-slate-600 rounded-full flex items-center"
            @click="showDropdown = !showDropdown"
          >
            <img
              src="https://www.tekoway.com/wp-content/uploads/2018/12/John-Doe.jpg"
              alt=""
              class="mr-2 w-6 h-6 rounded-full"
            />
            <p class="font-semibold text-white text-xs">John Doe</p>
            <i
              v-if="!showDropdown"
              class="fa-solid fa-sort-down text-white ms-2 mb-1"
            ></i>
            <i v-else class="fa-solid fa-sort-up text-white ms-2 mt-2"></i>
          </button>
          <div
            v-if="showDropdown"
            class="absolute bg-slate-600 w-full rounded mt-1"
          >
            <button
              @click="showDropdown = false"
              class="w-full py-2 text-slate-300 hover:text-white border-b border-slate-400 text-sm"
            >
              Account
            </button>
            <button
              @click="showDropdown = false"
              class="w-full py-2 text-slate-300 transition hover:text-white text-sm"
            >
              Log out
            </button>
          </div>
        </div>
      </div>
      <!-- cards -->
      <div class="px-6 py-4">
        <div class="flex justify-between items-center mb-5">
          <h1
            class="text-2xl font-semibold text-white tracking-wider hover:underline"
          >
            Recently Played
          </h1>
          <h2
            class="text-xs text-slate-300 uppercase tracking-wider hover:underline"
          >
            See All
          </h2>
        </div>
        <div class="w-full flex flex-wrap">
          <div v-for="recent in recents" class="py-2 mr-3 w-48 relative">
            <div
              class="absolute w-full h-full flex justify-end items-end p-8 opacity-0 hover:opacity-100 transition-opacity"
            >
              <div
                class="bg-green-600 rounded-full h-10 w-10 flex items-center justify-center hover:cursor-pointer"
              >
                <i class="fa-solid fa-play text-2xl ms-1"></i>
              </div>
            </div>
            <div class="bg-slate-600 w-full h-auto p-5 rounded-lg shadow">
              <img :src="recent.src" class="w-full h-36 shadow mb-2" alt="" />
              <h3 class="text-sm font-semibold text-white tracking-wider">
                {{ recent.title }}
              </h3>
              <h4 class="text-xs tracking-wide text-slate-300 pb-4">
                {{ recent.artist }}
              </h4>
            </div>
          </div>
        </div>
      </div>
      <div class="px-6 py-4">
        <div class="">
          <h1
            class="text-2xl font-semibold text-white tracking-wider hover:underline"
          >
            Made for Stephanie
          </h1>
          <h2 class="text-sm text-slate-400">
            Get better recomendations the more your listen.
          </h2>
        </div>
        <div class="w-full flex flex-wrap">
          <div v-for="recent in recents" class="py-2 mr-3 w-48 relative">
            <div
              class="absolute w-full h-full flex justify-end items-end p-8 opacity-0 hover:opacity-100 transition-opacity"
            >
              <div
                class="bg-green-600 rounded-full h-10 w-10 flex items-center justify-center hover:cursor-pointer"
              >
                <i class="fa-solid fa-play text-2xl ms-1"></i>
              </div>
            </div>
            <div class="bg-slate-600 w-full h-auto p-5 rounded-lg shadow">
              <img :src="recent.src" class="w-full h-36 shadow mb-2" alt="" />
              <h3 class="text-sm font-semibold text-white tracking-wider">
                {{ recent.title }}
              </h3>
              <h4 class="text-xs tracking-wide text-slate-300 pb-4">
                {{ recent.artist }}
              </h4>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- play bar -->
  <div class="w-full bg-zinc-900 h-20 flex items-center justify-between px-3">
    <div class="flex items-center">
      <div>
        <h1 class="mb-1 text-sm text-white tracking-wide">
          Summer in the City - Remastered
        </h1>
        <h2 class="text-xs text-slate-500 tracking-wide">
          The Lovin' Spoonfull
        </h2>
      </div>
      <i class="fa-solid fa-heart text-green-500 mx-4 text-xl"></i>
      <i class="material-icons text-slate-400 text-xl hover:text-white"
        >picture_in_picture_alt</i
      >
    </div>
    <div class="flex flex-col justify-center">
      <div class="flex items-center mx-auto">
        <button class="text-slate-600 hover:text-white">
          <i class="text-lg material-icons">shuffle</i>
        </button>
        <button class="mx-3 text-slate-600 hover:text-white">
          <i class="text-lg material-icons">skip_previous</i>
        </button>
        <button @click="playToggle" class="text-slate-600 hover:text-white">
          <i v-if="!pause" class="material-icons text-5xl"
            >play_circle_outline</i
          >
          <i v-else="pause" class="material-icons text-5xl">pause</i>
        </button>
        <button class="mx-3 text-slate-600 hover:text-white">
          <i class="text-lg material-icons">skip_next</i>
        </button>
        <button class="text-slate-600 hover:text-white">
          <i class="text-lg material-icons">repeat</i>
        </button>
      </div>
      <div class="w-96 rounded-full h-1 bg-slate-400 mt-1 flex items-center">
        <div class="h-1 rounded-full w-24 bg-green-600"></div>
        <div
          class="w-5 h-5 rounded-full bg-green-800 flex items-center justify-center shadow"
        >
          <div class="w-3 h-3 rounded-full bg-slate-400"></div>
        </div>
      </div>
    </div>
    <div class="flex items-center">
      <i class="material-icons text-slate-400 text-xl hover:text-white"
        >playlist_play</i
      >
      <i class="material-icons text-slate-400 text-xl mx-3 hover:text-white"
        >important_devices</i
      >
      <i class="material-icons text-slate-400 text-xl hover:text-white"
        >volume_up</i
      >
      <div class="w-20 ml-3 rounded-full bg-slate-600 h-1"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      pages: [
        {
          id: "home",
          name: "Home",
          icon: "fa-solid fa-house",
        },
        {
          id: "search",
          name: "Search",
          icon: "fa-solid fa-magnifying-glass",
        },
        {
          id: "library",
          name: "Your Library",
          icon: "fa-regular fa-chart-bar",
        },
      ],
      setId: "home",
      albums: [
        { name: "drive" },
        { name: "zhu" },
        { name: "All new indie" },
        { name: "Mellow" },
        { name: "Classic" },
        { name: "Lana Del Rey Radio" },
      ],
      showDropdown: false,
      pause: false,
      recents: [
        {
          src: "https://source.unsplash.com/random/500×500/?music/1",
          title: "Daily Mix 1",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/2",
          title: "Daily Mix 2",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/3",
          title: "Daily Mix 3",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/4",
          title: "Daily Mix 4",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/5",
          title: "Daily Mix 5",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/6",
          title: "Daily Mix 6",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/7",
          title: "Daily Mix 7",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/8",
          title: "Daily Mix 8",
          artist: "By Spotify",
        },
        {
          src: "https://source.unsplash.com/random/500×500/?music/9",
          title: "Daily Mix 9",
          artist: "By Spotify",
        },
      ],
    };
  },
  methods: {
    playToggle() {
      if (!this.pause) {
        this.$refs.audioPlayer.play();
      } else {
        this.$refs.audioPlayer.pause();
      }

      this.pause = !this.pause
  
    },
  },
};
</script>

<style scoped></style>
