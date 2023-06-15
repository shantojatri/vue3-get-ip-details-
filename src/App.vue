<script setup lang="ts">
import { ref } from "vue";
import axios from "axios";

const detailsValue = ref<Array>([]);

// const getIp = ref<String>('');
// const getIpAddress = async() => { 
//   await axios.get(`https://api.ipify.org/?format=json`)
//     .then((res) => {
//     console.log(res.data.ip)  
//     getIp.value = res.data.ip
//   });  
// }

// const getDetails2 = async (ip) => {
//   await axios.get(`http://ip-api.com/json/${ip}`)
//   .then((res) => {  
//     detailsValue.value = res.data 
//   });  
// }

// const getAll2 = () => { 
//   Promise.all([getIpAddress()]).then(() => {
//     getDetails2(getIp.value)
//   })
//   .finally(()=> console.log('Ended2'));
// }
// getAll2();


const getDetails = async () => {
  await axios.get(`http://ip-api.com/json/`)
  .then((res) => {  
    detailsValue.value = res.data 
  });  
}

/**
 * This function is way better than getAll2, for getting IP details
 */
const getAll = () => { 
  Promise.all([getDetails()]).then()
  .finally(()=> console.log('Ended'));
}
getAll();
</script>

<template>
  <header>  
    <div class="wrapper">  
      <div v-if="detailsValue?.status === 'success'">
        <div v-if="detailsValue?.countryCode === 'BD'">
          দেশঃ বাংলাদেশ 
          ভাষাঃ বাংলা 
        </div>
        <div v-else>
          Country: {{ detailsValue?.country }}
          Language: English
        </div>
      </div>

      <h1>Get IP Address Details: </h1>
      <p>{{ detailsValue }}</p>

    </div>
  </header> 
</template>
