<template>
    <div class="card">
        <div class="media">
            <img :src="media" />
        </div>
         <div class="card-body">
            <div class="card-title"  v-bind:style="{ color: color}">{{ renderTitle }}</div>
            <div class="card-desc">{{ renderDesc }}</div>
             <a :href="url" target="_blank" v-if="more" class="card-more"><span>more</span></a>
         </div>
        
    </div>
</template>
<script>

export default {
    props:{
        media:{
            type:String,
        },
        title:{
            type: String,
            default: 'Hello world Lorem ipsum dolor sit amet'
        },
        description:{
            type: String,
            default: 'Lorem ipsum dolor sit amet, his eu ubique graeco eruditi, ex civibus ue elaboraret'
        },        
        color: {
            type: String,
            default:'#444'
        },
         url:{
            type: String,
            default: '#'
        },
    },
    data(){
       return{
            more: false
       }
    },
    computed: {
        renderDesc(){
        
            if(this.description.length > 100){
                //  this.more= !this.more;
                return this.description.substring(0,100)+"...";
            }
            return this.description;
        } ,
         renderTitle(){
            if(this.title.length > 25){
                return this.title.substring(0,25)+"...";             
            }
            return this.title;
        }    
    }
}

</script>

<style scoped>
  .card{
       box-sizing: content-box;
       margin: 20px 5px;
       background: #FFF;
       border: 1px solid #eee;
       overflow: hidden;
       width: 250px;
       min-height: 300px;
         border-radius: 4px;
         /* box-shadow: 0 2px 4px 0 rgba(0, 0, 0, .06); */
box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
/* -moz-box-shadow: 0 3px 1px -2px rgba(0,0,0,.2), 0 2px 2px 0 rgba(0,0,0,.14), 0 1px 5px 0 rgba(0,0,0,.12);
-webkit-box-shadow: 0 3px 1px -2px rgba(0,0,0,.2), 0 2px 2px 0 rgba(0,0,0,.14), 0 1px 5px 0 rgba(0,0,0,.12);
box-shadow: 0 3px 1px -2px rgba(0,0,0,.2), 0 2px 2px 0 rgba(0,0,0,.14), 0 1px 5px 0 rgba(0,0,0,.12); */


        -webkit-transition: -webkit-box-shadow .2s, -webkit-transform .2s;
         -o-transition: box-shadow .2s, transform .2s, -o-transform .2s;
         transition: box-shadow .2s, transform .2s;
         transition: box-shadow .2s, transform .2s, -webkit-box-shadow .2s, -webkit-transform .2s, -o-transform .2s;
     }
     .card:hover{
        -webkit-box-shadow: 0 2px 6px 0 rgba(0, 0, 0, .06), 0 3px 12px 0 rgba(0, 0, 0, .12);
    box-shadow: 0 2px 6px 0 rgba(0, 0, 0, .06), 0 3px 12px 0 rgba(0, 0, 0, .12);
    -webkit-transform: translateY(-10px);
    -ms-transform: translateY(-10px);
    -o-transform: translateY(-10px);
    transform: translateY(-10px);
     }
     .card .media{
         width: 100%;
         height: 180px;
         margin: 0;
         padding: 0;
         overflow: hidden;
     }
     .card .media img{
         width: 100%;
         height: 100%;
         background: #ccc;
         
     }
     .card-body{
         width: 100%;
         height: 120px;
         margin: 0;
         padding: 0px;
         background: #FFF;
     }
     .card-title{
       padding: 10px;
       font-weight: bold;
     }
     .card-desc{
       padding: 10px 10px 0px 10px;
       text-align: justify;
       font-size: 14px;
       color: #777;
     }
     .card-footer{       
         margin: 0;
         background: coral;
     }
     .card-more{
         text-decoration: none;

         font-size: 11px;
         padding: 2px 5px;
         border: 1px solid #999;
         color: #999;
         float: right;
         margin: 2px 5px;
         cursor: pointer;
     }
</style>
