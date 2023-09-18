<!-- <template>
  <div>
    <h1>{{ pageTitle }}</h1>
    <img :src="artist.image" :alt="artist.name" />
    <div v-for="artist of artists" :key="artist.id">
      <nuxt-link :to="`/artists/${artist.id}`" @click="changeImage(artist)">
        {{ artist.name }}
      </nuxt-link>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const pageTitle = `Artist of ${route.params.id}`;

const artists = ref([
  { id: "1", name: "John Doe", image: "https://via.placeholder.com/100x300" },
  { id: "2", name: "Jane Doe", image: "https://via.placeholder.com/200x300" },
  { id: "3", name: "John Smith", image: "https://via.placeholder.com/300x300" },
]);

const changeImage = (artist) => {
  artist.image = "https://via.placeholder.com/200x200";
};
</script> -->


<template>
  <h1>{{ pageTitle }}</h1>

  <div class="text-3xl">
    {{ artist.name }}
  </div>

  <div v-for="song in artist.songs" :key="song.id">
    <div class="text-2xl">
      {{ song.title }}
    </div>
  </div>






  <!-- <img :src="image" :alt="artists[0].name" />
  <div v-for="artist of artists" :key="artist.id">
    <nuxt-link :to="`/artists/${artist.id}`">{{ artist.name }}</nuxt-link>
    <div @click="change(artist.image)">
      {{ artist.name }}
    </div>
  </div>
  <button @click="change">Change</button> -->
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const pageTitle = `Artist of ${route.params.id}`;
const {data:artist} = await useLazyFetch<any>(`http://localhost/api/artist/${route.params.id}`);
const image = ref<string>("image");
image.value = "https://via.placeholder.com/300x300";

const change = function(_image: string) {
  image.value = _image
};

const artists = [
  { id: "1", name: "John Doe", image: "https://via.placeholder.com/100x300" },
  { id: "2", name: "Jane Doe", image: "https://via.placeholder.com/200x300" },
  { id: "3", name: "John Smith", image: "https://via.placeholder.com/300x300" },
];
</script>
