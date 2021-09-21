<template>
  <div id="app">
    <main class="page-container">
      <header class="page-header">
        <h1 class="card2">Simple Flashcard App</h1>
      </header>

      <AddNewCard @addCardTrigger="addCard"></AddNewCard>
      <p class="card2"></p>
      <a href="#" class="card3 max-w-sm text-2xl font-bold leading-tight">
        <span class="link link-underline link-underline-black text-blue-50"> You have liked {{ likes }} cards so far </span>
      </a>


      <p class="card2"></p>
      <a href="#" class="font-display max-w-sm text-2xl font-bold leading-tight">
        <span class="link link-underline link-underline-black text-black"> Click on the Flashcards to see them change </span>
      </a>
      <ul class="grid grid-cols-6 gap-4">
        <Card
            v-for="card in filteredData"
            :key="card.id"
            :card="card"
            @likeTrigger="recalculateLikes"
            @deleteTrigger="deleteCard"
        ></Card>
      </ul>
      <!-- end of cards box -->
      <p class="card2"></p>





      <a href="#" class="card3 max-w-sm text-2xl font-bold leading-tight">
        <span class="link link-underline link-underline-white text-blue-50">
        Enjoy!
      </span>
      </a>
      <p class="card2"></p>
    </main>
  </div>
</template>

<script>

import AddNewCard from "../components/AddNewCard";
import Card from "../components/Card";

const uuidv4 = require("uuid/v4");
const colors = ["-orange", "-red", "-purple", "-blue", "-green"];

let cards = [
  {
    id: uuidv4(),
    front: "First front: Lorem ipsum and Lorem ipsum🤔",
    back: "First back Lorem ipsum and Lorem ipsum 😎",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"

  },
  {
    id: uuidv4(),
    front: "One and a half front Lorem ipsum and Lorem ipsum 🤭",
    back: "One half back Lorem ipsum and Lorem ipsum🤣",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"
  },
  {
    id: uuidv4(),
    front: "second - front Lorem ipsum and Lorem ipsum✔️",
    back: "sec backLorem ipsum and Lorem ipsum 📅",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"
  },
  {
    id: uuidv4(),
    front: "third front Lorem ipsum and Lorem ipsum💻",
    back: "third back Lorem ipsum and Lorem ipsum🔥",
    flipped: false,
    liked: true,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"
  },
  {
    id: uuidv4(),
    front: "forth front Lorem ipsum and Lorem ipsum😱",
    back: "forth back Lorem ipsum and Lorem ipsum😂",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"
  },
  {
    id: uuidv4(),
    front: "fifth frontLorem ipsum and Lorem ipsum😊",
    back: "firth back Lorem ipsum and Lorem ipsum",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"
  },
  {
    id: uuidv4(),
    front: "sixth! Lorem ipsum and Lorem ipsum🤩",
    back: "sixth back Lorem ipsum and Lorem ipsum🔥",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"
  },
  {
    id: uuidv4(),
    front: "seventh Lorem ipsum and Lorem ipsum✏️",
    back: "seventh back Lorem ipsum and Lorem ipsum Lorem ipsum and Lorem ipsum",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`,
    symbollike : "❤️",
    dislike : "👎"
  }
];

export default {
  name: "app",
  data() {
    return {
      cards: cards,
      searchWord: "",
      likes: cards.filter(card => card.liked).length
    };
  },
  methods: {
    searchCards(keyword) {
      this.searchWord = keyword;
    },
    recalculateLikes(value) {
      value ? this.likes++ : this.likes--;
    },
    deleteCard(id) {
      this.cards = this.cards.filter(card => {
        if (card.id === id && card.liked) {
          this.likes--;
        }
        return card.id !== id;
      });
    },
    addCard(data) {
      this.cards.unshift(data);
    }
  },
  computed: {
    filteredData() {
      return this.cards.filter(card => {
        return card.front
            .toLowerCase()
            .includes(this.searchWord.trim().toLowerCase());
      });
    }
  },
  components: {
    AddNewCard,
    Card
  }
};
</script>
<style lang="scss" scoped>

.wrapper {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
.card {
  @apply p-10 rounded-lg text-emerald-500 bg-emerald-100 shadow-lg;
  .title {
    @apply text-6xl font-bold;
  }
}
.card2{
  @apply p-12 rounded-lg text-blue-50 bg-blue-800 shadow-lg;
  .title {
    @apply text-6xl font-bold;
  }
}
.card3{
  @apply p-12 rounded-lg text-blue-50 bg-gray-600 shadow-lg;
  .title {
    @apply text-6xl font-bold;
  }
}
.link-underline {
  border-bottom-width: 0;
  background-image: linear-gradient(transparent, transparent), linear-gradient(#fff, #fff);
  background-size: 0 3px;
  background-position: 0 100%;
  background-repeat: no-repeat;
  transition: background-size .5s ease-in-out;
}

.link-underline-black {
  background-image: linear-gradient(transparent, transparent), linear-gradient(#A2C, #A2C)
}


.link-underline-purp {
  background-image: linear-gradient(transparent, transparent), linear-gradient(#F11, #F30)
}

.link-underline:hover {
  background-size: 100% 3px;
  background-position: 0 100%
}
</style>
