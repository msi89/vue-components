<template>
 <transition name="fade" appear>
    <div class="coral-drawer" v-if="show">
        <div class="coral-drawer-menu" v-bind:style="{  background: background}">
            <slot></slot>
        </div>
        <div class="coral-drawer-shadow" @mousedown="Close"></div>
    </div>
 </transition>
</template>
<script>
export default {
    props:{
        background:{
            type: String,
            default:'coral'
        }, 
        size:{
            type: Number,
            default:300
        }, 
    },
    data(){
        return{
            show:true
        }
    },
    mounted() {       
        //    var screen_width=window.screen.availWidth;
        //    let shadow= document.querySelector(".coral-drawer-shadow");   
        //    var s=    (this.size*100)/screen_width;
        //    shadow.style.width = (100-s) +"%";            
    },
    methods:{
        Close(){
            this.show = !this.show;
            console.log(this.show);
        }
    }
}
</script>

<style>
 .coral-drawer{
     width: 100%;
     height: 100%;
     margin: 0;
     padding: 0;
     position: fixed;
     z-index: 10000;
 }

 .coral-drawer-shadow {
    height: 100%;
    width: 75%;
    z-index: 100;
    float: left;
    background-color: rgba(0, 0, 0, 0.5);
}
.coral-drawer-menu {
    height: 100%; 
    width: 25%;
    z-index: 100; 
    float: left;
    background-color: coral; 
    overflow-x: hidden; 
    padding-top: 60px; 
    text-align: center;
    transition: 0.5s; 
}
.fade-enter-active, .fade-leave-active{
    transition: width 0.5s, transform 0.5s;
}
.fade-enter, .fade-leave-active{
    width: 0%;
    /* transform: translateX(-300px); */
}
</style>


