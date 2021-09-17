<template>
  <div id="app">
    <main class="page-container">
      <header class="page-header">

        <!-- end of top message -->
        <h1 class="card2">Simple Flashcard App</h1>
        <Search @searchTrigger="searchCards"></Search>
      </header>
      <!-- end of page header -->
      <AddNewCard @addCardTrigger="addCard"></AddNewCard>
      <p class="card2">You have liked {{ likes }} cards so far</p>
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
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
  },
  {
    id: uuidv4(),
    front: "One and a half front Lorem ipsum and Lorem ipsum 🤭",
    back: "One half back Lorem ipsum and Lorem ipsum🤣",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
  },
  {
    id: uuidv4(),
    front: "second - front Lorem ipsum and Lorem ipsum✔️",
    back: "sec backLorem ipsum and Lorem ipsum 📅",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
  },
  {
    id: uuidv4(),
    front: "third front Lorem ipsum and Lorem ipsum💻",
    back: "third back Lorem ipsum and Lorem ipsum🔥",
    flipped: false,
    liked: true,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
  },
  {
    id: uuidv4(),
    front: "forth front Lorem ipsum and Lorem ipsum😱",
    back: "forth back Lorem ipsum and Lorem ipsum😂",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
  },
  {
    id: uuidv4(),
    front: "fifth frontLorem ipsum and Lorem ipsum😊",
    back: "firth back Lorem ipsum and Lorem ipsum",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
  },
  {
    id: uuidv4(),
    front: "sixth! Lorem ipsum and Lorem ipsum🤩",
    back: "sixth back Lorem ipsum and Lorem ipsum🔥",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
  },
  {
    id: uuidv4(),
    front: "seventh Lorem ipsum and Lorem ipsum✏️",
    back: "seventh back Lorem ipsum and Lorem ipsum Lorem ipsum and Lorem ipsum",
    flipped: false,
    liked: false,
    color: `${colors[Math.floor(Math.random() * colors.length)]}`
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
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
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
</style>
