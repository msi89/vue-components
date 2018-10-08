<template>
    <div>
         <h2>Toast message</h2>
        <Toast :message=" msg " background="#fff" color="coral" v-if="toasted" />
        <button class="btn" @click="toast()">Test</button>

        <h2>alert</h2>
        <Alert  background="coral" title="C'est moi" message="Hello everyone" color="#fff" delai="14" position="top-center"  v-if="cas"></Alert>
        <Alert  background="#10ac84" color="#fff" delai="14" position="top-right"  v-if="cas1"></Alert>
        <Alert  background="#f368e0" color="#fff" delai="14" position="top-left"  v-if="cas2"></Alert>
        <Alert  background="#8395a7" color="#fff" delai="14" position="bottom-center"  v-if="cas3"></Alert>
        <Alert  background="#222f3e" color="#fff" delai="14" position="bottom-right"  v-if="cas4"></Alert>
        <Alert  background="#0abde3" color="#fff" delai="14" position="bottom-left"  v-if="cas5"></Alert>
        <button class="btn" @click="alert()">Top center</button>
        <button class="btn" @click="alert1()">Top right</button>
        <button class="btn" @click="alert2()">Top left</button>
        <button class="btn" @click="alert3()">Bottom center</button>
        <button class="btn" @click="alert4()">Bottom right</button>
        <button class="btn" @click="alert5()">Bottom left</button>

<h2>Card</h2>
<div class="grid">
    <!-- <div class="item" v-for="(photo,i) in photos" :key="i"> -->
      <Card  v-for="(photo,i) in photos" :key="i" :media="photo.urls.thumb"/>
    <!-- </div> -->
</div>
</div>
</template>
<script>
import Alert from '@/components/Alert.vue'
import Toast from '@/components/Toast.vue'
import Card from '@/components/Card.vue'
import axios from 'axios'

var accessKey = '0b1bd5a140a6b95e27f5a6e5c67c70e9858ece622955ffb135c314bad5fa0c65';
var secretKey = 'd156f43a8fdc2a0a48753c7953527f9b795c575723e21a5504b91b747569c6b6';
 var options = {
        params: {
          client_id: accessKey,
          page: 15,
          per_page: 15
        }
    }

const Api = axios.create({
  baseURL: 'https://api.unsplash.com'
});
export default {
    components:{
        Alert,
        Toast,
        Card
    },
  
    data(){
        return{
            cas: false,
            cas1: false,
            cas2: false,
            cas3: false,
            cas4: false,
            cas5: false,
            toasted:false,
            msg:'Hi, i am toast',
            photos:[]
        }
    },
    methods:{
        toast(){
            this.toasted = !this.toasted;
            this.msg= "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.";
        },
        alert(){
            this.cas = !this.cas;
        },
        alert1(){
            this.cas1 = !this.cas1;
        },           
        alert2(){
            this.cas2 = !this.cas2;
        },   
        alert3(){
            this.cas3 = !this.cas3;
        },
        alert4(){
            this.cas4 = !this.cas4;
        },
        alert5(){
            this.cas5 = !this.cas5;
        },
        getPhotos() {    
             Api.get('/photos',options)
            .then(response => (this.photos = response.data))
            .catch(error => console.log(error))
        }
    },
    created: function() {
       this.getPhotos()
    }

}
</script>
<style scoped>
  .grid {
    width: 100%;
    max-width: 1280px;
    display: flex;
    justify-content:center;
    flex-wrap: wrap; 
  }
.grid .item{
    float: left;
}
</style>


