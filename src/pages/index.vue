<template>
    <div>
        <h2>Toast</h2>
        <Toast  background="coral" title="C'est moi" message="Hello everyone" color="#fff" delai="14" position="top-center"  v-if="alert"></Toast>
        <Toast  background="#10ac84" color="#fff" delai="14" position="top-right"  v-if="alert1"></Toast>
        <Toast  background="#f368e0" color="#fff" delai="14" position="top-left"  v-if="alert2"></Toast>
        <Toast  background="#8395a7" color="#fff" delai="14" position="bottom-center"  v-if="alert3"></Toast>
        <Toast  background="#222f3e" color="#fff" delai="14" position="bottom-right"  v-if="alert4"></Toast>
        <Toast  background="#0abde3" color="#fff" delai="14" position="bottom-left"  v-if="alert5"></Toast>
        
        <button class="btn" @click="toast()">Top center</button>
        <button class="btn" @click="toast1()">Top right</button>
        <button class="btn" @click="toast2()">Top left</button>
        <button class="btn" @click="toast3()">Bottom center</button>
        <button class="btn" @click="toast4()">Bottom right</button>
        <button class="btn" @click="toast5()">Bottom left</button>
    </div>
</template>
<script>
import Toast from '@/components/Toast.vue'
export default {
    components:{
        Toast
    },
   
    data(){
        return{
            alert: false,
            alert1: false,
            alert2: false,
            alert3: false,
            alert4: false,
            alert5: false,
        }
    },
    methods:{
        toast(){
            this.alert = !this.alert;
        },
        toast1(){
            this.alert1 = !this.alert1;
        },           
        toast2(){
            this.alert2 = !this.alert2;
        },   
        toast3(){
            this.alert3 = !this.alert3;
        },
        toast4(){
            this.alert4 = !this.alert4;
        },
        toast5(){
            this.alert5 = !this.alert5;
        }
    }

}
</script>
<style scoped>
 
</style>


