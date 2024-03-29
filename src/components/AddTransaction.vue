<template>
     <h3>Add new transaction</h3>
      <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
          <label for="text">Text</label>
          <input type="text" id="text" v-model="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
          <label for="ammount"
            >Amount <br />
            (negative - expense, positive - income)</label
          >
          <input type="text" id="ammount" v-model="ammount" placeholder="Enter ammount..." />
        </div>
        <button class="btn">Add transaction</button>
      </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';
const text = ref('');
const ammount = ref('');
const emit = defineEmits(['transactionSubmitted']);
const toast = useToast();

const onSubmit = () => {
    if(!text.value || !ammount.value) {
        toast.error('Both fields must be filled');
        return;
    }
    const transactionData = {
        text: text.value,
        ammount: parseFloat(ammount.value),

    };
    emit('transactionSubmitted', transactionData);

    text.value = '';
    ammount.value = '';
};
</script>