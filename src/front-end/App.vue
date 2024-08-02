<script setup lang="ts">
import { onMounted, ref } from 'vue';


const openExternal = (url: string) => {

     console.log('openExternal', url);
     window.electronAPI.openExternal(url);
 }


 const luckyNumber = ref(-1);
 const menuCounter = ref(0);

onMounted(async () => {
    getLuckyNumber();
    
    
    window.electronAPI.onUpdateMenuCounter((value) => {
        menuCounter.value += value;
    });

});


const getLuckyNumber = async () => {
    const number = await window.electronAPI.getRandomNumber();
    luckyNumber.value = number;
}



</script>

<template>


    <h1>Electron Forge Starter Kit</h1>

    <button @click="openExternal('https://www.electronjs.org/')">Open Electron Website</button>

    <span>Your Lucky Number: {{ luckyNumber !== -1 ? luckyNumber : 'Wait for it...' }}</span>
    <span>Menu Counter: {{ menuCounter }}</span>
    
    <RouterView></RouterView>

</template>