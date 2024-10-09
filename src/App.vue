<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import axios, {type AxiosResponse} from 'axios';
import {ref} from "vue";

interface gameItem {
    title: string,
    thumbnail: string,
    short_description: string,
    game_url: string,
    genre: string,
    platform: string,
    publisher: string,
    developer: string,
    release_date: string,
    freetogame_profile_url: string,
}

const items = ref<gameItem[]>()

let getgames = ()=>{
  axios.get('https://free-to-play-games-database.p.rapidapi.com/api/games', {
    headers: {
      'x-rapidapi-host': 'free-to-play-games-database.p.rapidapi.com',
      'x-rapidapi-key': '64352bef0fmshb80aebb8909bd6bp1f0ee5jsn2ef21fad2f67'
    }
  }).then((response: AxiosResponse) =>
  {
    items.value = response.data;
    console.log(response.data)
  });
}
getgames()
</script>

<template>
  <header>
    <ul class="flex flex-wrap">
      <li v-for="item in items" class="m-20">
      {{ item.title }}
    <img :src=item.thumbnail>
      {{ item.short_description }}<br>
    <a :href=item.game_url class="text-blue-500">{{ item.game_url }}</a><br>
      {{ item.genre }}<br>
      {{ item.platform }}<br>
      {{ item.publisher }}<br>
      {{ item.developer }}<br>
      {{ item.release_date }}<br>
    <a :href=item.freetogame_profile_url class="text-blue-500">{{ item.freetogame_profile_url }}</a>
    </li>
</ul>
  </header>

  <RouterView />
</template>
