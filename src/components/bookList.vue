<template>
  <div class="text-start pt-60">
    <span class="header heading-style">Lorem Ipsum</span>

    <div class="row pt-4">
      <div class="card">

        <VueSlickCarousel @init="sliderLoaded" v-bind="settings" :arrows="true" :dots="true">
          <div class="card zoom-img" @click="selectedBook(book)" v-for="book in booksList" :key="book.title">
            <img width="250" class="br-16" :src="require(`@/assets/books/${book.book_image}`)" :alt="book.book_image">
            <div class="bottom-left book-details inline-grid image-text">
              <span class="book-name"> {{ book.title }} </span>
              <span class="book-author-publisher-list"> {{ book.author }} </span>
              <span class="book-author-publisher-list"> {{ book.publisher }} </span>
            </div>
            <div class="top-right book-rating " style="color : white"> {{book.rating}} out of 5 </div>
          </div>
        </VueSlickCarousel>
      </div>
    </div>


    <div id="navigateHere" class="row pt-4" v-if="showBookDetails">
      <div class="column">
        <span class="selected-book-name"> {{selectedBookDetails.title}} </span> <br> <br>
        <img class="selected-book-image mt-14 br-6" :src="require(`@/assets/books/${selectedBookDetails.book_image}`)"
          alt=""> <br>

        <button @click="showSnackbar" class="mt-14 btn default ">Add To Favorites +</button>
      </div>
      <div class="column">
        <div class="row">
          <div class="column">
            <span class="selected-book-author"> {{selectedBookDetails.author}} </span> <br>
            <span class="selected-book-publisher"> {{ selectedBookDetails.publisher }} </span> <br> <br>
            <span class="selected-book-description"> {{ selectedBookDetails.description }} </span> <br>
          </div>
          <div class="column">
            <img @click="close" style="float : right" src="../assets/close.png" alt="search">
          </div>
        </div>

      </div>
    </div>

    <div id="snackbar"> {{selectedBookDetails.title}} added to favorites! </div>
  </div>

</template>


<script>
import VueSlickCarousel from 'vue-slick-carousel'
import 'vue-slick-carousel/dist/vue-slick-carousel.css'
// optional style for arrows & dots
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'

import list from "../../books.json";
export default {
  name: 'BookList',
  components: { VueSlickCarousel },
  data() {
    return {
      booksList: list.results.books,
      settings: {
        "infinite": true,
        "speed": 500,
        "slidesToShow": 4,
        "slidesToScroll": 4,
        "initialSlide": 0,
        "responsive": [
          {
            "breakpoint": 600,
            "settings": {
              "slidesToShow": 1,
              "slidesToScroll": 1,
            }
          },
          {
            "breakpoint": 480,
            "settings": {
              "slidesToShow": 1,
              "slidesToScroll": 1
            }
          }
        ]
      },
      showBookDetails: false,
      selectedBookDetails : {}
    }
  },
  methods: {
    selectedBook(e) { 
      this.selectedBookDetails = e;
      this.showBookDetails = true;
      setTimeout(() => { window.location = "#navigateHere"; }, 100);
    },
    close() {
      this.showBookDetails = false;
    },
    showSnackbar() {
      var snackBar = document.getElementById("snackbar");
      snackBar.className = "show";
      setTimeout(function () { snackBar.className = snackBar.className.replace("show", ""); }, 3000);
    },
    sliderLoaded() {
      setTimeout(() => { document.getElementsByClassName('slick-dots')[0].remove(); },100 )
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header{
  font-size: 32px;
    font-weight: inherit;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.125;
    letter-spacing: normal;
    color: #fff;
    margin: 0 0 16px;
}
.text-start{
  text-align: start;
}
.pt-60{
  padding-top: 60px;
}

.heading-style{
  text-transform: uppercase;
  font-size: larger;
}

* {
  box-sizing: border-box;
}

.card{
  position: relative;
    text-align: center;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

.card:hover {
  transform: scale(1);
  /* (150% zoom - Note: if the zoom is too large, it will go outside of the viewport) */
}

.bottom-left {
  position: absolute;
  bottom: 22px;
  left: 16px;
}

.top-right {
  position: absolute;
  top: 15px;
  right: 25px;
}

.inline-grid{
  display: inline-grid;
}

.br-16{
  border-radius: 16px;
}

.image-text{
  position: absolute;
    bottom: 16px;
    background: rgb(0, 0, 0);
    background: rgba(0, 0, 0, 0.8);
    color: #f1f1f1;
    width: 86%;
    padding: 6px 6px 23px 0px;
    border-bottom-right-radius: 16px;
    border-bottom-left-radius: 16px;
}

/* On book list */
.book-name{
  font-size: 18px;
    font-weight: 500;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.2;
    letter-spacing: -.2px;
    color: #fff;
    max-width: 100%;
    margin: 0 0 7px;
}

.book-author-publisher-list{
  font-size: 13px;
    font-weight: 300;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.4;
    letter-spacing: .4px;
    color: hsla(0, 0%, 100%, .9);
}

.book-rating{
  background: #003366;
    opacity: 0.90;
    font-size: 16px;
    font-weight: 100;
    font-stretch: normal;
    font-style: normal;
    line-height: normal;
    letter-spacing: .2px;
    color: #fff;
    border-top-right-radius: 16px;
    border-bottom-left-radius: 10px;
    padding : 6px
}

.book-details{
  text-align: left;
    padding-left: 8px;
}



/* on book selected */

.selected-book-name{
  font-size: 40px;
    font-weight: 100;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.2;
    letter-spacing: .6px;
    /* color: #555452; */
    margin-bottom: 40px;
    margin-top: 0;
    max-width: 360px;
    text-align: left;
}

.selected-book-image{
  width: 60px;
    border-radius: 4px;
    object-fit: cover;
}

.selected-book-author{
  font-size: 18px;
    font-weight: 500;
    font-stretch: normal;
    font-style: normal;
    line-height: normal;
    letter-spacing: normal;
    color: #fff;
    margin-bottom: 2px;
}

.selected-book-publisher{
  font-size: 14px;
    font-weight: 300;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.44;
    letter-spacing: .43px;
    color: hsla(0, 0%, 100%, .6);
}

.selected-book-description{
  font-family: Helvetica Neue LT W05_45 Light;
    font-size: 14px;
    font-weight: 300;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.36;
    letter-spacing: .4px;
    color: hsla(0, 0%, 100%, .7);
    width: 50px;
    word-break: break-word;
}


.pt-4{
  padding-top: 12px !important;
}

.mt-14{
  margin-top: 14px;
}

.br-6{
  border-radius : 6px
}




.column {
  float: left;
  width: 50%;
  padding: 10px;
  height: 300px;
  /* Should be removed. Only for demonstration */
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

/* Remove extra left and right margins, due to padding in columns */
.row {
  margin: 0 -5px;
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

.btn {
  border: none;
  color: white;
  padding: 14px 28px;
  font-size: 16px;
  cursor: pointer;
}

.default {
  background-color: #4e4c4c;
  color: white;
  border-radius: 4px;
}

/* Gray */
.default:hover {
  background: rgb(100, 100, 100);
}

/* Style the counter cards */
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  /* this adds the "card" effect */
  padding: 16px;
  text-align: center;
  /* background-color: #f1f1f1; */
}

/* Responsive columns - one column layout (vertical) on small screens */
@media screen and (max-width: 600px) {
  .column {
    width: 100%;
    display: block;
    margin-bottom: 20px;
  }
  .book-rating{
    right: 0px;
  }
  .image-text{
    width: 95%;
  }
}

/* snackbar css */
#snackbar {
  visibility: hidden;
  min-width: 250px;
  margin-left: -125px;
  background-color: #04AA6D;
  color: #fff;
  text-align: center;
  border-radius: 2px;
  padding: 16px;
  position: fixed;
  z-index: 1;
  left: 50%;
  bottom: 30px;
  font-size: 17px;
}

#snackbar.show {
  visibility: visible;
  -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
  animation: fadein 0.5s, fadeout 0.5s 2.5s;
}

@-webkit-keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }

  to {
    bottom: 30px;
    opacity: 1;
  }
}

@keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }

  to {
    bottom: 30px;
    opacity: 1;
  }
}

@-webkit-keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }

  to {
    bottom: 0;
    opacity: 0;
  }
}

@keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }

  to {
    bottom: 0;
    opacity: 0;
  }
}


/* Zoom Image */
.zoom-img img:hover {
  border : 2px solid white
}
</style>
