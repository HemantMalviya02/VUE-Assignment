<script setup>
import blackwidow from "./assets/images2/blackwidow.jpg";
import marvel from "./assets/images2/captainmarvel.jpg";
import gamora from "./assets/images2/gamora.jpg";
import scarlet from "./assets/images2/scarletwitch.jpg";
import wasp from "./assets/images2/wasp1.jpg";
import shuri from "./assets/images2/shuri.jpg";


let ladyAvengers = [
          {
            "title": "Wasp",
            "firstname": "Janet",
            "lastname": "Van Dyne",
            "movies": [
              { "title": "Ant-Man", "year": 2015 },
              { "title": "Ant-Man and the Wasp", "year": 2018 },
              { "title": "Avengers: Endgame", "year": 2019 }
            ],
            "image": wasp,
            // "color": "warning",
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
            ],
            "image": scarlet,
            // "color": "info",
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
            ],
            "image": blackwidow,
            // "color": "danger",
          },
          {
            "title": "Captain Marvel",
            "firstname": "Carol",
            "lastname": "Danvers",
            "movies": [
              { "title": "Captain Marvel", "year": 2019 },
              { "title": "Avengers: Endgame", "year": 2019 }
            ],
            "image": marvel,
            // "color":"primary",
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
            ],
            "image": gamora,
            // "color": "warning",
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
            ],
            "image": shuri,
            // "color": "secondary",
          }
        ]
let bgcolors = ["#f4ff12", "#f3acf6", "#5dade2", " #d5d8dc", "#f07474", "#7fb3d5"]
</script> 

<template>
<div class="container py-5">
  <h1>Avengers carousel</h1> <br>
  <div id="heroCarousel" class="carousel slide" data-bs-ride="carousel" data-bs-interval="2000">
    <div class="carousel-inner">
      <div class="carousel-item" :class="{active:idx===0}" :style="{backgroundColor: bgcolors[idx % bgcolors.length]}" v-for="(avengers, idx) in ladyAvengers" :key="idx"> 
        <h1 class="mb-4">{{avengers.title}}</h1>
        <div class="row">
          <div class="col-md-3">
            <div class="object-fit-cover border rounded">
                <img :src = "avengers.image" height="320px" width="304px">
            </div>
          </div>
          <div class="col-md-9">
            <h2 class="fw-bold">{{avengers.firstname +" "+ avengers.lastname}}</h2>
            <hr>
            <ul class="list-unstyled fs-5">
              <li v-for="(movie, idx) in avengers.movies" :key="idx">{{movie.title}}</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <div class="carousel-indicators mt-4">
      <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
      <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="1" aria-label="Slide 2"></button>
      <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="2" aria-label="Slide 3"></button>
      <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="3" aria-label="Slide 4"></button>
      <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="4" aria-label="Slide 5"></button>
      <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="5" aria-label="Slide 6"></button>
    </div>
  </div>
</div>
</template>

<style scoped>
    hero-image {
      background-color: black;
      color: white;
      width: 100%;
      height: 300px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2rem;
    }
    .carousel-indicators [data-bs-target] {
      background-color: #000;
    }
    
</style>

// , 'bg-'+ avengers.color]