<script setup>
  import {ref ,computed, watch, onMounted} from 'vue'

  const tombol = ref(null)

  const teks = ref('')

  const lists = ref([
    {id : 1, text : "Olahraga", status : true},
    {id : 2, text : "Makan" , status : true},
    {id : 3, text : "Tidur", status : false}
  ])

  function tambahkan(){
    let isi = {
      id : lists.value.length + 1,
      text : teks.value,
      status : false
    }

    lists.value.push(isi)
    teks.value = ''
  }

  const selesai = computed(() => {
    return lists.value.filter((x) => x.status == true)
  })

  const belum = computed(() => {
    return lists.value.filter((x) => x.status == false)
  })

  const nomor = ref(2)

  watch(nomor , (a , b) => {
    if(a > 16){
    console.log("Data nya berubah dari "+b+" menjadi " + a)
    nomor.value.setAttribute("disabled",true)
    }
  })

  const kata = ref(null)

  onMounted(() => {
    kata.value.textContent = 'Ari kristian'
  })

</script>

<template>

<input type="text" v-model="teks">
<button v-on:click="tambahkan" :disabled="teks == ''">submit</button>

<h2>Semua</h2>
<ul>
  <li v-for="list in lists"> {{ list.id }}. {{ list.text }} : {{ list.status }}
    <input type="checkbox" v-model="list.status">
  </li>
</ul>

<h2>Sudah</h2>
<ul>
  <li v-for="list in selesai"> {{ list.id }}. {{ list.text }} 
  </li>
</ul>

<h2>Belum</h2>
<ul>
  <li v-for="list in belum"> {{ list.id }}. {{ list.text }} 
  </li>
</ul>

<button ref="tombol" v-on:click="nomor*=2">click : {{ nomor }}</button>

<p ref="kata">Hallo</p>

</template>


<style scoped>

</style>
