<template>
       <div>
        <div class="auth-shadow">

        </div>
            <!-- <transition name="fade" appear> -->
                <div  class="ui-auth">
                    <h4>Please sign in</h4>
                    <div class="ui-auth-error">{{ message }}</div>
                    <div class="form-field"><input type="text" placeholder="-- username --" v-model="$store.state.auth.username"></div>     
                    <div class="form-field"><input type="password" placeholder="-- password --" v-model="$store.state.auth.password"></div>                    
                    <div class="ui-auth-btn">                       
                            <button @click="submit">Sign in</button>                      
                            <button @click="reset">Cancel</button>
                    </div>
                   
                </div>
            <!-- </transition> -->
       </div>
</template>
<script>
export default {
    props:{
        message:''
    },
     methods:{
        submit() {
           this.$emit('submit');
        },
         reset() {
           this.$emit('reset');
        },
         anim() {
             var ui= document.querySelector(".ui-auth");
        
            // setInterval(()=>{
                ui.style.display='block';
                ui.style.marginTop='0px'
         // }, 2000)
        },
        
    },
    data(){
        return {
            username:'',
            password:'',
            error:false
        }
    }
   ,mounted() {
         this.anim();
    }
}
</script>
<style scoped>
.auth-shadow{
     z-index: 1000;
    position: fixed;
    width: 100%;
    height: 100%;
    overflow: hidden;
    padding: 0;
    margin: 0;
      top: 0;
      left: 0;
    background: rgba(0,0,0,0.2);
}
.ui-auth{
    display: none;
    z-index: 1001;
    width: 400px;
    position: absolute;
    padding: 10px;
    border-radius: .0em;
    margin: 0px auto; 
    overflow-x: hidden;
    top: 0;   
    left: 0;
    right: 0;
    background: #fff;;
    box-shadow: 0 2px 2px 0 rgba(0,0,0,0.2);
    margin-top: -100px;
    transition: margin-top 0.25s ease-in;
}

.ui-auth:hover {
 box-shadow: 0 2px 2px 0 rgba(0,0,0,0.3);
}
.ui-auth h4{
    margin-left: 20px;
    margin-bottom: 10px;
}

/* On screens that are 600px wide or less, make the columns stack on top of each other instead of next to each other */
@media screen and (max-width: 700px) {
  .ui-auth {
    width: 90%;
    margin: 0px auto;
  }
}
@media screen and (min-width: 701px) {
  .ui-auth {
    width: 400px;
    margin: 0px auto;
    margin-top: -1px;
  }
}
.ui-auth .form-field{
    width: 90%;
    margin: 0px auto;
}
.form-field{
   margin: 0px auto;
}
.form-field input{
    outline: none;
    height: 25px;
    width: 100%;
    margin: 2px 0px;
    padding: 2px 5px;
    border: 1px solid #ccc;
}
.form-field input:focus{
    border: 1px solid lightblue;
    color:#555;
}
.ui-auth-btn{
    float: right;
    margin-right: 20px;
    margin-top: 2px;
}
.ui-auth-btn button{
    background-color: #ccc;
    border: 1px solid #AAA;
    padding: 2px 5px;
    cursor: pointer;
    outline: none;;
    transition: background-color 0.3s;
}
.ui-auth-error{
    color: crimson;
    font-size: 12px;
}
.ui-auth-btn button:hover{
    background-color: rgb(213, 223, 223);
}
.ui-auth-btn button:active{
    background-color: #AAA;
}
.fade-enter-active, .fade-leave-active{
    transition: opacity 0.5s, transform 0.5s;
}
.fade-enter, .fade-leave-active{
    opacity: 0;
    transform: translateY(-100px);
}
</style>


