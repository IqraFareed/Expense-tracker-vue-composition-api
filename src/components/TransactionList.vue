<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      :class="t.amount < 0 ? 'minus' : 'plus'"
      v-for="t in transactions"
      :key="t.id"
    >
      {{ t.text }} <span>${{ t.amount }}</span>
      <button @click="deleteTransaction(t.id)" class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from "vue";
const emit = defineEmits(["transactionDeleted"]);
const props = defineProps({
  transactions: {
    type: Number,
    required: true,
  },
});

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};

////////////// options api//////////////
// data() {
//   return {
//     transations: [
//       { id: 1, text: "Flower", amount: -19.99 },
//       { id: 2, text: "Salary", amount: 299.97 },
//       { id: 3, text: "Book", amount: -10 },
//       { id: 4, text: "Camera", amount: 150 },
//     ],
//   };
// },
// };
</script>
