<script setup>
/*
I tried to create a handy webapp to keep track of all the movies I've watched this year and which was my favorite, but form bindings are confusing and it's not working properly :(

Can you help me fix it?

level 1: Update the movie list with a v-for loop so all movies in the provided file movies.json are rendered. Feel free to update/change the list to your likes, or to add more info for each movie.

level 2: Create a small "movie card" for each movie object in the list and display in it the title, a small poster picture, and the score of the movie.

level 3: Remove the duplicated & hardcoded code in the form binding for "My fav movie" selector, and use a v-for loop and attribute bindings to correctly build the options. (Note: you can change the binding variable 'favoriteMovie' below if needed)

level 4: I want it to be easy to see which one is my current favorite, so please add a "😍" emoji next to the title to my favorite movie in the list.

level 5: The score of each film is represented by a string with a value between "0" and "100". We can do better! Let's show between 1 to 5 stars in each film card, according to the score (tip: use a v-for loop here).

level 6: Fix the multiselectors of the movies I've watched this year. Remove the duplicated & hardcoded code in the form binding for both multi selectors, and use v-for loops and attribute bindings to correctly build the options. Keep in mind they should be synchronized! (keep using the same binding to the variable "watchedList" for both fields).

level 7: The multiselectors are nice, but it would be great to also have a checkbox on each film card to mark it as watched/not watched. Of course, it should be synchronized with the "watchedList" array!

bonus level: Apply your CSS magic and designer's touch to make the app look great!
*/

import { ref } from 'vue';
import movies from './assets/movies.json';

const favoriteMovie = ref('');
const watchedList = ref([]);

console.log(watchedList);
</script>

<template>
  <h3>Movie list</h3>
  <div class="post">
    <div class="poster" v-for="(movie, i) in movies" :key="movie.id">
      <img :src="movie.picture" :alt="movie.title" />
      <div class="movie__title">{{ movie.title }}</div>
      <div class="movie__score">
        <svg
          v-for="_ in parseInt((movie.score * 5) / 100)"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          width="16"
          height="16"
        >
          <defs>
            <linearGradient
              id="b"
              x1="-1483.396"
              x2="-1155.767"
              y1="1056.787"
              y2="1056.787"
              gradientUnits="userSpaceOnUse"
              xlink:href="#a"
            />
            <linearGradient id="a">
              <stop offset="0" stop-color="#fcd635" />
              <stop offset="1" stop-color="#f7a928" />
            </linearGradient>
          </defs>
          <path
            fill="url(#b)"
            d="M-1220 1212.362c-11.656 8.326-86.446-44.452-100.77-44.568-14.324-.115-89.956 51.449-101.476 42.936-11.52-8.513 15.563-95.952 11.247-109.61-4.316-13.658-76.729-69.655-72.193-83.242 4.537-13.587 96.065-14.849 107.721-23.175 11.656-8.325 42.535-94.497 56.86-94.382 14.323.116 43.807 86.775 55.327 95.288 11.52 8.512 103.017 11.252 107.334 24.91 4.316 13.658-68.99 68.479-73.527 82.066-4.536 13.587 21.133 101.451 9.477 109.777z"
            color="#000"
            overflow="visible"
            transform="matrix(.04574 0 0 .04561 68.85 -40.34)"
            style="marker: none"
          />
        </svg>
      </div>
      <div class="checkbox">
        <input
          type="checkbox"
          :id="'option' + i"
          :value="movie.title"
          v-model="watchedList"
        />
        Watched
      </div>
    </div>
  </div>

  <hr />
  <h3>Controls</h3>
  <div>
    <span>My fav movie: {{ favoriteMovie || 'none chosen yet :( ' }}</span>
    <br />
    <br />
    <select @input="(select) => (favoriteMovie = select.target.value)">
      <option disabled value="">Please select a favorite!</option>
      <option v-for="movie in movies" :value="movie.title" :key="movie.id">
        {{ movie.title }}
        <template v-if="favoriteMovie == movie.title">😍</template>
      </option>
    </select>
  </div>

  <hr />

  <div>
    <span>Movies watched this year: {{ watchedList }}</span>
    <br />
    <br />
    <select v-model="watchedList" multiple>
      <option v-for="movie in movies" :key="movie.id">
        {{ movie.title }}
      </option>
    </select>
  </div>

  <hr />
  <div>
    <span>Movies watched this year: {{ watchedList }}</span>
    <br />
    <br />

    <div v-for="(movie, i) in movies" :key="movie.id">
      <input
        type="checkbox"
        :id="'option' + i"
        :value="movie.title"
        v-model="watchedList"
      />
      <label :for="'option' + i">{{ movie.title }}</label>
      <br />
    </div>
  </div>
</template>

<style scoped>
.post {
  display: flex;
  flex-direction: column;
}

.poster {
  margin-bottom: 10px;
}

.post img {
  height: 150px;
  width: 100px;
  border-radius: 10px;
  float: left;
  margin-right: 10px;
}

.movie__title {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 10px;
}
</style>
