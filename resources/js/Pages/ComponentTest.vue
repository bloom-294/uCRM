<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';

const emitTest = (e) => {
  console.log(e);
}

</script>

<template>
  <GuestLayout>
    最近怎么样？
    <InputLabel value="💐">💐</InputLabel>
    <TextInput model-value="我不错！" @update:model-value="emitTest"></TextInput>
  </GuestLayout>

</template>
