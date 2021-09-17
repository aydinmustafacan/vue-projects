<template>
  <div>
    <div class="card">
      <label>
        <input
          v-model="front"
          :class="{ '-error': error }"
          type="text"
          class="input"
          placeholder="Front"
        />
      </label>
      <label>
        <input
          @keypress.enter="addCard"
          v-model="back"
          type="text"
          class="input"
          :class="{ '-error': error }"
          placeholder="Back"
        />
      </label>
      <button class="btn" @click="addCard()" type="button">
        Add a new card
      </button>
    </div>
    <!-- end of add card box -->

  </div>
</template>

<script>
const uuidv4 = require("uuid/v4");
const colors = ["-orange", "-red", "-purple", "-blue", "-green"];

export default {
  name: "AddNewCard",
  data() {
    return {
      front: "",
      back: "",
      error: false
    };
  },
  methods: {
    addCard() {
      if (!this.front || !this.back) {
        this.error = true;
      } else {
        const card = {
          id: uuidv4(),
          front: this.front,
          back: this.back,
          flipped: false,
          liked: false,
          color: `${colors[Math.floor(Math.random() * colors.length)]}`
        };
        this.$emit("addCardTrigger", card);
        this.front = "";
        this.back = "";
        this.error = false;
      }
    }
  }
};
</script>
<style lang="scss" scoped>
.btn {
  @apply px-4 py-2 text-gray-500 rounded-lg hover:bg-emerald-100 hover:text-emerald-700;

  &.nuxt-link-exact-active {
    @apply bg-emerald-100 text-emerald-700;
  }
}
</style>

