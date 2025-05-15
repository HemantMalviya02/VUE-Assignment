<script setup>
import { computed, ref } from 'vue';

    let ladyAvengers = [
          {
            "title": "Wasp",
            "firstname": "Janet",
            "lastname": "Van Dyne",
            "movies": [
              { "title": "Ant-Man", "year": 2015 },
              { "title": "Ant‑Man and the Wasp", "year": 2018 },
              { "title": "Avengers: Endgame", "year": 2019 }
            ]
          },
          {
            "title": "Scarlet Witch",
            "firstname": "Wanda",
            "lastname": "Maximoff",
            "movies": [
              { "title": "Captain America: The Winter Soldier", "year": 2014 },
              { "title": "Avengers: Age of Ultron", "year": 2015 },
              { "title": "Captain America: Civil War", "year": 2016 },
              { "title": "Avengers: Infinity War", "year": 2018 },
              { "title": "Avengers: Endgame", "year": 2019 },
              { "title": "Doctor Strange in the Multiverse of Madness", "year": 2022 }
            ]
          },
          {
            "title": "Black Widow",
            "firstname": "Natasha",
            "lastname": "Romanoff",
            "movies": [
              { "title": "Iron Man 2", "year": 2010 },
              { "title": "Avengers", "year": 2012 },
              { "title": "Captain America: The Winter Soldier", "year": 2014 },
              { "title": "Avengers: Age of Ultron", "year": 2015 },
              { "title": "Captain America: Civil War", "year": 2016 },
              { "title": "Avengers: Infinity War", "year": 2018 },
              { "title": "Avengers: Endgame", "year": 2019 }
            ]
          },
          {
            "title": "Captain Marvel",
            "firstname": "Carol",
            "lastname": "Danvers",
            "movies": [
              { "title": "Captain Marvel", "year": 2019 },
              { "title": "Avengers: Endgame", "year": 2019 }
            ]
          },
          {
            "title": "Gamora",
            "firstname": "Gamora Zen",
            "lastname": "Whoberi Ben Titan",
            "movies": [
              { "title": "Guardians of the Galaxy", "year": 2014 },
              { "title": "Guardians of the Galaxy Vol. 2", "year": 2017 },
              { "title": "Avengers: Infinity War", "year": 2018 },
              { "title": "Avengers: Endgame", "year": 2019 }
            ]
          },
          {
            "title": "Shuri",
            "firstname": "Shuri",
            "lastname": "Princess",
            "movies": [
              { "title": "Black Panther", "year": 2018 },
              { "title": "Avengers: Infinity War", "year": 2018 },
              { "title": "Avengers: Endgame", "year": 2019 },
              { "title": "Black Panther: Wakanda Forever", "year": 2022 }
            ]
          }
        ]

const searchData = ref("");
const filterData = computed(() => {
  const searchQuery = searchData.value.toLowerCase();
  return ladyAvengers.filter(v => {

    console.log(v.movies.map(v => v.title).some(movie => movie.toLowerCase().includes(searchQuery)));
    
    // v.movies.map(v => v.title) this is for converting the array to object
    //.some(movie => movie.toLowerCase().includes(searchQuery)) is used to apply filter on the above object
    
    return (
      v.firstname.toLowerCase().includes(searchQuery) || v.lastname.toLowerCase().includes(searchQuery) || v.title.toLowerCase().includes(searchQuery) || v.movies.map(v => v.title).some(movie => movie.toLowerCase().includes(searchQuery))
    );
  })
});
</script>

<template>
    <div class="container">
      <h1>Search Filter</h1>
      <i class="fa-solid fa-magnifying-glass ml-5"></i>
      <input type="text" v-model="searchData" placeholder="search here">
      <br><br>

      <div v-if="filterData.length" class="card text-white bg-dark mb-3" style="width: 50rem;">
          <div v-for="(hero, idx) in filterData" :key="idx" class="card-header">{{hero.title}}
          <div class="card-body">
            <h5 class="card-title">{{ hero.firstname +" "+ hero.lastname }}</h5>
            <ul v-for="(movie, i) in hero.movies" :key="i" > 
              <li>{{ movie.title +" released in "+ movie.year}}</li>
            </ul>
          </div>
          </div>
      </div>
    </div>
</template>

<style scoped>

</style>
