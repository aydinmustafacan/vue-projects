<template>
  <li class="card">
      <article
        @click="flipCard(card, $event)"
      >
        <button type="button" @click="deleteCard(card.id)">
          🗑️
        </button>
        <br/>
        <h2>{{ card.flipped ? card.back : card.front }}</h2>
        <br/>
        <button
          type="button"
          @click="likeCard(card)"
        >
          ❤️
        </button>
      </article>
  </li>
</template>

<script>
export default {
  name: "Card",
  props: ["card"],
  methods: {
    flipCard(card) {
        card.flipped = !card.flipped;
    },
    deleteCard(id) {
      this.$emit("deleteTrigger", id);
    },
    likeCard(card) {
      card.liked = !card.liked;
      this.$emit("likeTrigger", !!card.liked);
    }
  }
};
</script>

<style>
.icon{
  color: brown;
  padding: 10px;
  font-size: 48px;
}
.card-box{
  border-color: aqua;
  border-style: dashed;

}
</style>
