<template>
  <div class="screen-panel">
    <div class="sound-player">
      <div class="book-panel">
        <BookImage v-for="book in booksVisible" :key="book.id" :bookImage="book.isbn" :selectedBookNumber="selectedBookNumber" :bookNumber="book.id" :bookBackColor="book.color" @select-current = "selectCurrent">{{ book.title }}</BookImage>
      </div>
    <!--  <BookControls :startBookNumber="startBookNumber" :selectedBook="selectedBook" @increase-by="increaseCount"></BookControls>-->
      <div>
        &nbsp;
      </div>
      <div class="page-panel">
        <PageImage v-for="(page, index) in pagesVisible" :key="page" :selectedBookNumber="selectedBookNumber" :selectedPageNumber="selectedPageNumber" :pageNumber="index + startPageNumber" :pageBackColor="booksVisible[selectedBookNumber].color" :pageId="page" :soundId="soundsVisible[index]" @play-audio="onPlayAudio" @stop-all-audios="onStopAllAudios" @select-current-page="selectCurrentPage">{{ page }}
        </PageImage>
      </div>
<!--      <PageControls :selectedBookNumber="selectedBookNumber" :selectedPageNumber="selectedPageNumber" :selectedPage="pagesVisible[selectedPageNumber]" :soundId="soundsVisible[selectedPageNumber]" @increase-by="increasePageCount"></PageControls>-->
    </div>
    <textarea id="myTextArea"></textarea>
  </div>
</template>

<style scoped>
.screen-panel {
  width: 100vw;
  height: 100vh;
  //border: dashed 5px red;
}

.sound-player {
  display: flex;
  flex-direction: column;
  width: 90vw;
  //border: dashed 5px purple;
}

.book-panel {
  display: flex;
  flex-wrap: wrap;
}

.page-panel {
  display: flex;
  flex-wrap: wrap;
}

textarea {
  width: 80vw;
  height: 50vh;
}

</style>

<script setup>
import BookImage from './BookImage.vue'
import PageImage from './PageImage.vue'
import BookControls from './BookControls.vue'
import PageControls from './PageControls.vue'

import { ref } from 'vue'

let id = 0;
let numBooksVisible = 8;
let booksVisible = [];
const startBookNumber = ref(0);
const selectedBookNumber = ref(2);
let selectedBook = {};
let pagesColor = "pink";

let numPagesVisible = 12;
let pagesVisible = [];
let soundsVisible = [];
let numPages = 0;

const startPageNumber = ref(0);
const selectedPageNumber = ref(0);

const books = [
  { id: id++, title: 'Thomas and Gordon', color: 'red',         isbn: '50010000.jpg', sounds: ['40010001','40010002','40010003','40010004','40010005','40010006','40010007','40010008','40010009','40010010','40010011','40010012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas Train', color: 'skyblue',          isbn: '50020000.jpg', sounds: ['40020001','40020002','40020003','40020004','40020005','40020006','40020007','40020008','40020009','40020010','40020011','40020012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Harold', color: 'yellow',      isbn: '50030000.jpg', sounds: ['40030001','40030002','40030003','40030004','40030005','40030006','40030007','40030008','40030009','40030010','40030011','40030012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Annie', color: 'green',        isbn: '50040000.jpg', sounds: ['40040001','40040002','40040003','40040004','40040005','40040006','40040007','40040008','40040009','40040010','40040011','40040012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Gordon', color: 'skyblue',     isbn: '50050000.jpg', sounds: ['40050001','40050002','40050003','40050004','40050005','40050006','40050007','40050008','40050009','40050010','40050011','40050012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Percy', color: 'red',          isbn: '50060000.jpg', sounds: ['40060001','40060002','40060003','40060004','40060005','40060006','40060007','40060008','40060009','40060010','40060011','40060012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Henry', color: 'green',        isbn: '50070000.jpg', sounds: ['40070001','40070002','40070003','40070004','40070005','40070006','40070007','40070008','40070009','40070010','40070011','40070012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Clarabelle', color: 'skyblue', isbn: '50080000.jpg', sounds: ['40080001','40080002','40080003','40080004','40080005','40080006','40080007','40080008','40080009','40080010','40080011','40080012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Annie', color: 'green',        isbn: '50090000.jpg', sounds: ['40090001','40090002','40090003','40090004','40090005','40090006','40090007','40090008','40090009','40090010','40090011','40090012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Fattie', color: 'skyblue',     isbn: '50100000.jpg', sounds: ['40100001','40100002','40100003','40100004','40100005','40100006','40100007','40100008','40100009','40100010','40100011','40100012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Cronk', color: 'yellow',       isbn: '50110000.jpg', sounds: ['40110001','40110002','40110003','40110004','40110005','40110006','40110007','40110008','40110009','40110010','40110011','40110012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Daisy', color: 'yellow',       isbn: '50120000.jpg', sounds: ['40120001','40120002','40120003','40120004','40120005','40120006','40120007','40120008','40120009','40120010','40120011','40120012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Toby', color: 'skyblue',       isbn: '50130000.jpg', sounds: ['40130001','40130002','40130003','40130004','40130005','40130006','40130007','40130008','40130009','40130010','40130011','40130012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Rocky', color: 'red',          isbn: '50140000.jpg', sounds: ['40140001','40140002','40140003','40140004','40140005','40140006','40140007','40140008','40140009','40140010','40140011','40140012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Harry', color: 'skyblue',      isbn: '50150000.jpg', sounds: ['40150001','40150002','40150003','40150004','40150005','40150006','40150007','40150008','40150009','40150010','40150011','40150012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
  { id: id++, title: 'Thomas and Elisa', color: 'red',          isbn: '50160000.jpg', sounds: ['40160001','40160002','40160003','40160004','40160005','40160006','40160007','40160008','40160009','40160010','40160011','40160012'], pages: ['50010001','50010002','50010003','50010004','50010005','50010006','50010007','50010008','50010009','50010010','50010011','50010012']},
];

createBooksVisible();

function createBooksVisible() {
  booksVisible = books.slice(startBookNumber.value, startBookNumber.value + numBooksVisible);
  selectedBook = books[selectedBookNumber.value];
  createPagesVisible();
}

function createPagesVisible() {
  numPages = books[selectedBookNumber.value].pages.length;
  pagesVisible = books[selectedBookNumber.value].pages.slice(startPageNumber.value, startPageNumber.value + numPagesVisible);
  soundsVisible = books[selectedBookNumber.value].sounds.slice(startPageNumber.value, startPageNumber.value + numPagesVisible);
}
function increaseCount(n) {
  selectedBookNumber.value = selectedBookNumber.value + n;
  if(selectedBookNumber.value < 0) {
    selectedBookNumber.value = 0;
  }

  if(selectedBookNumber.value >= books.length) {
    selectedBookNumber.value = books.length - 1;
  }

  if(n > 0) {
    if(selectedBookNumber.value > (startBookNumber.value + numBooksVisible - 1)) {
      startBookNumber.value = startBookNumber.value + 1;
    }
  }

  if(n < 0) {
    if(selectedBookNumber.value < startBookNumber.value) {
      startBookNumber.value  = selectedBookNumber.value;
    }
  }

  createBooksVisible();
  selectedPageNumber.value = 0;
  startPageNumber.value = 0;
  createPagesVisible();
}

function selectCurrent(bookNumber) {
  selectedBookNumber.value = bookNumber;
  selectedBook = books[bookNumber];
  startPageNumber.value = 0;
  pagesVisible = books[selectedBookNumber.value].pages.slice(startPageNumber.value, startPageNumber.value + numPagesVisible);
  soundsVisible = books[selectedBookNumber.value].sounds.slice(startPageNumber.value, startPageNumber.value + numPagesVisible);
  selectedPageNumber.value = 0;
}

function selectCurrentPage(pageNumber) {
  selectedPageNumber.value = pageNumber;
  // playNextAudio();
}

function increasePageCount(n) {
  console.log("selectedPageNumber.value = ", selectedPageNumber.value, "startPageNumber.value = ", startPageNumber.value, "n = ", n)
  selectedPageNumber.value = selectedPageNumber.value + n;
  if(selectedPageNumber.value < 0) {
    selectedPageNumber.value = 0;
  }

  if(selectedPageNumber.value >= numPages) {
    selectedPageNumber.value = numPages - 1;
  }

  if(n > 0) {
    if(selectedPageNumber.value > (startPageNumber.value + numPagesVisible - 1)) {
      startPageNumber.value = startPageNumber.value + 1;
    }
  }

  if(n < 0) {
    if(selectedPageNumber.value < startPageNumber.value) {
      startPageNumber.value  = selectedPageNumber.value;
    }
  }

  createPagesVisible();
}

// let soundCounter = 10000001;
// let audio = new Audio('https://my.anglik.pl/sounds/' + soundCounter++ + '.wav');
// let timeout = null;
// let duration = 0;
//
// audio.addEventListener("loadeddata", () => {
//   if(timeout) {
//     clearTimeout(timeout);
//   }
//   duration = audio.duration;
//   console.log("loadedDuration", duration, "| soundCounter", soundCounter);
//   timeout = setTimeout(playNextAudio, (duration * 1000 + 2000));
// });
//
// function playNextAudio() {
//   audio.src = 'https://my.anglik.pl/sounds/' + soundCounter++ + '.wav';
//   audio.play();
//   console.log("playedDuration", duration, "| soundCounter", soundCounter);
// }

function onStopAllAudios(pageNumber) {
  // alert('I will stop all audios playing now: ' + pageNumber);
  const textarea = document.getElementById("myTextArea");

  selectedPageNumber.value = pageNumber;

  soundsVisible.forEach(page => {
    // console.log("checking to pause: ", page)
    const myAudio = document.getElementById(page);
    if(!myAudio.paused) {
      myAudio.pause();
      console.log("pausing: ", page)
      textarea.value += "Pausing sound id: " + page + "\n";
    }
  });
  // const myAudio = document.getElementById(soundId);
}

function onPlayAudio(pageNumber, soundId) {
  const textarea = document.getElementById("myTextArea");
  console.log("Pressed to play: ", soundId);
  textarea.value += "Pressed to play SoundId:" + soundId + "\n";
  onStopAllAudios(pageNumber);
  console.log("Now Playing PageNumber: ", pageNumber, " SoundId:", soundId);
  const myAudio = document.getElementById(soundId);
  myAudio.currentTime = 0
  myAudio.play();

  textarea.value += "Now Playing PageNumber: " + pageNumber + " SoundId:" + soundId + "\n";
}

</script>