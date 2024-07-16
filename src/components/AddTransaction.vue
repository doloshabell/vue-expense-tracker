<template>
  <h3>Add New Transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="class-control">
      <label for="text">Text</label>
      <input
        type="text"
        id="text"
        v-model="textDesc"
        placeholder="Enter text..."
      />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />(negative - expense, positive - income)</label
      >
      <input
        type="text"
        v-model="amount"
        id="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add Transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const textDesc = ref("");
const amount = ref("");
const toast = useToast();
const emit = defineEmits(["transactionSubmitted"]);

const onSubmit = () => {
  if (!textDesc.value || !amount.value) {
    toast.error("Both fields must be filled");
    return;
  }

  const transactionData = {
    textDesc: textDesc.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmitted", transactionData);

  textDesc.value = "";
  amount.value = "";
};
</script>
