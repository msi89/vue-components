<template>
     <!-- <div class="ui"> -->
         <transition name="fade" appear>
          <div class="ui-toast"   v-if="visible" v-bind:style="{ color: color, background: background }">      
              <div class="ui-toast-message">{{ renderMessage }}</div>      
          </div>
         </transition>
       
     <!-- </div> -->
</template>
<script>
export default {
    name:'Toast',
    props:{
      
        message:{
            type: String,
            default:'Lorem Ipsum is simply dummy text of the printing and typesetting industry.'
        },       
        background:{
            type: String,
            default:'#FFF'
        },        
        color: {
            type: String,
            default:'gray'
        },        
    },
    data (){
        return{
            visible:true,
            timer:'',
            delai: 3,
            msg:''
        }
    },
    methods:{
        toggle(){
            this.visible = !this.visible;
        }
    },
    computed:{
        renderMessage(){
            if(this.message.length > 55){
                return  this.message.substring(0,55)+"...";
            }
            return this.msg;           
        }
    },
    mounted() {
       
        
       this.timer = setInterval(()=>{
           this.delai--;
              if(this.delai == 0){
                   this.visible = false;
                   this.delai=0;
              }
        }, 1000)
    },
    destroyed() {
        clearInterval(this.timer);
        this.time=0;
    },
}
</script>


<style scoped>

.ui-toast{
    z-index: 1000;
    position: absolute;
    width: 400px;
    height: 40px;
    position: absolute;
    padding: 10px;
    border-radius: .0em;
    margin: 0px auto; 
    top: 0;   
    left: 0;
    right: 0;
    box-shadow: 0 2px 2px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
}

.ui-toast:hover {
 box-shadow: 0 2px 2px 0 rgba(0,0,0,0.3);
}

/* On screens that are 600px wide or less, make the columns stack on top of each other instead of next to each other */
@media screen and (max-width: 700px) {
  .ui-toast {
    width: 90%;
    margin: 0px auto;
  }
}
@media screen and (min-width: 701px) {
  .ui-toast {
    width: 400px;
    margin: 0px auto;
    margin-top: -1px;
  }
}


.ui-toast-message{
    width: 350px;
    line-height: 40px;
    text-align: center;
    font-size: 14px;
}

.fade-enter-active, .fade-leave-active{
    transition: opacity 0.5s, transform 0.5s;
}
.fade-enter, .fade-leave-active{
    opacity: 0;
    transform: translateY(-30px);
}
</style>
