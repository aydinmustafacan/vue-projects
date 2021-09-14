<template>
  <h1>App by Mustafa Aydin</h1>
  <form @submit.prevent="addItem()">
    <label>New Item</label>
    <input
        v-model="newItem"
        name="newItem"
        autocomplete="off"
    >
    <button>Add an Item</button>
  </form>
  <h2>List</h2>
  <ul>
    <li
        v-for="(itemm, index) in items"
        :key="index"
    >
      <span>{{ itemm.content }}</span>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';
export default {
  name: 'App',
  setup () {
    const newItem = ref('');
    const defaultData = []
    const itemsData = JSON.parse(localStorage.getItem('items')) || defaultData;
    const items = ref(itemsData);
    function addItem () {
      if (newItem.value) {
        items.value.push({
          content: newItem.value
        });
        newItem.value = '';
      }
      saveData();
    }
    function saveData () {
      const storageData = JSON.stringify(items.value);
      localStorage.setItem('items', storageData);
    }
    return {
      items,
      newItem,
      addItem,
      saveData
    }
  }
}
</script>

<style lang="scss">
$border: 2px solid
rgba(
    $color: white,
    $alpha: 0.35,
);
$size1: 6px;
$size2: 12px;
$size3: 18px;
$size4: 24px;
$size5: 48px;
$backgroundColor: #12124F;
$textColor: white;
$primaryColor: #86342d;
$secondTextColor: #1f2023;
body {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: $backgroundColor;
  color: $textColor;
  #app {
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
    padding: 20px;
    h1 {
      font-weight: bold;
      font-size: 28px;
      text-align: center;
    }
    form {
      display: flex;
      flex-direction: column;
      width: 100%;
      label {
        font-size: 14px;
        font-weight: bold;
      }
      input,
      button {
        height: $size5;
        box-shadow: none;
        outline: none;
        padding-left: $size2;
        padding-right: $size2;
        border-radius: $size1;
        font-size: 18px;
        margin-top: $size1;
        margin-bottom: $size2;
      }
      input {
        background-color: transparent;
        border: $border;
        color: inherit;
      }
    }
    button {
      cursor: pointer;
      background-color: $primaryColor;
      border: 1px solid $primaryColor;
      color: $secondTextColor;
      font-weight: bold;
      outline: none;
      border-radius: $size1;
    }
    h2 {
      font-size: 22px;
      border-bottom: $border;
      padding-bottom: $size1;
    }
    ul {
      padding: 10px;
      li {
        display: flex;
        justify-content: space-between;
        align-items: center;
        border: $border;
        padding: $size2 $size4;
        border-radius: $size1;
        margin-bottom: $size2;
        span {
          cursor: pointer;
        }

        button {
          font-size: $size2;
          padding: $size1;
        }
      }
    }
    h4 {
      text-align: center;
      opacity: 0.5;
      margin: 0;
    }
  }
}
</style>
