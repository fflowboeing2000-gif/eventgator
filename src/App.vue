<script setup>
import { ref } from 'vue'

const msg = ref('Hello World!')
const events = ref(
  [
  {id: 1, title: "Bookworm festival", desc: "Lorem ipsum", date: "30.11.25 11:30", i: "https://avatars.mds.yandex.net/i?id=0d0c02fa461573f0e7773159dfc6466bfd800984-7066126-images-thumbs&n=13"},
  {id: 2, title: "History of the Tea", desc: "Lorem ipsum", date: "30.11.25 12:30", i: "https://radarpekalongan.disway.id/upload/82d02e7ad92fcee121b2d96db780587e.jpg"},
  {id: 3, title: "Planes physics", desc: "Lorem ipsum", date: "11.12.25 16:20", i: "https://avatars.mds.yandex.net/i?id=609411854af7ac3645c52f163b7b3ea80e1874cd-5235884-images-thumbs&n=13"},
  {id: 4, title: "Films secrets", desc: "Lorem ipsum", date: "22.12.25 18:00", i: "https://avatars.mds.yandex.net/i?id=b99f9e916d3f9c0efcc748fb6b797e3e79cc40a2-12623317-images-thumbs&n=13https://avatars.mds.yandex.net/i?id=b99f9e916d3f9c0efcc748fb6b797e3e79cc40a2-12623317-images-thumbs&n=13"},
  {id: 4, title: "Programming tips", desc: "Lorem ipsum", date: "28.12.25 10:00", i: "https://avatars.mds.yandex.net/i?id=efd6f5fc8c557a81e56c599a7a9c79eb_l-6956316-images-thumbs&n=13"},
  ]
)

const showInfo = ref(false)
function showInfoWindow() {
  if (registered.value.length != 0) {
    showInfo.value = true
  }
}
// <Tab :title="msg" description="Libre dolor"></Tab>
const registered = ref([]);

var url = "https://barcodeapi.org/api/qr/"

function register(id){
  if (registered.value.indexOf(id) === -1) {
    registered.value.push(id)
  }else {
    return;
  }
}

function findById(id) {
  return events.value.indexOf(id)

}

</script>

<template>
  <div>
    <div class="upper">
        <h2>Events</h2>
        <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#1f1f1f" @click="showInfoWindow"><path d="M200-80q-33 0-56.5-23.5T120-160v-480q0-33 23.5-56.5T200-720h80q0-83 58.5-141.5T480-920q83 0 141.5 58.5T680-720h80q33 0 56.5 23.5T840-640v480q0 33-23.5 56.5T760-80H200Zm0-80h560v-480H200v480Zm280-240q83 0 141.5-58.5T680-600h-80q0 50-35 85t-85 35q-50 0-85-35t-35-85h-80q0 83 58.5 141.5T480-400ZM360-720h240q0-50-35-85t-85-35q-50 0-85 35t-35 85ZM200-160v-480 480Z"/></svg>
        
    
    </div>
    <p class="badge" v-if="registered.length">{{registered.length}}</p>
  </div>
  <div class="gr">

    <div class="card"  v-for="event in events" :key="event.id">

      <img :src="event.i"/>

      <h4>{{event.title}}</h4>

      <p>{{event.desc}}</p>

      <button type="button" @click="register(event.id)">Register <br>{{event.date}}</br></button>
    </div>

  </div>


  <div class="tickets" v-if="showInfo" @click="showInfo = false">
    <div class="overflow">
    <div class="window" v-for="ticket in registered">
      <h3>{{events[ticket-1].title}}</h3>
      <p>{{events[ticket-1].date}}</p>
      <div style='text-align: center;'>
      <img :src="url + ' ' + events[ticket-1].id +  events[ticket-1].date" />
    </div>  
    </div>
  </div>

  </div>
</template>

<style>

  body {
    margin: 0px;
    font-family: Helvetica;
  }

  .tickets {
    position:fixed;
    top: 0px;
    width: 100%;
    height: 100%;
    overflow: scroll;
    background-color: rgba(0,0,0,0.7);
    padding-top: 20px;
  }

  .window {
    padding: 10px;
    width: 60%;
    background-color: white;
    text-align: center;
    margin: auto;

  }

  .upper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-left: 20px;
    padding-right: 20px;
    z-index: 1;
  }

  .badge {
    color: white;
    position: absolute;
    top: -6px;
    height: 20px;
    z-index: 0;
    width: 20px;
    right: 10px;
    text-align: center;
    border-radius: 100px;
    
    background-color: #90A955;
  }

  .gr {
    display: grid;
    grid-template-columns: 1fr 1fr;
    
  }

  .card {
    border:2px solid #90A955;
    border-radius: 10px;
    padding: 15px;
    margin:10px;
  }

  button {
    background-color: #90A955;
    color: aliceblue;
    height: 50px;

    width: 100%;
    border-radius: 10px;
    border: none;
  }

  img {
    width: 100%;
    border-radius: 10px;
  }



  @media (max-width: 430px) {
    .gr {
      display: block;
    }
  }
</style>
