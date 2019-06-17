<script>
/* 
 how to use ?
<div id="app">
<!-- pagination -->
        <paginator
          :entries="entries" 
          :per-page="10"
          :color="paginatorColor"
          @data-changed="paginData"
        />
</div>
new Vue({
   el: '#app',
   data(){
     return {
       entries: [],
       paginEntries: [],
       paginatorColor: 'red'
     };
   },
   mounted(){
     this.getEntries();
   },
   methods:{
     getEntries() {
       for(var i=1; i<=1000;i++){
         this.entries.push({
           id:i, 
           name: 'John Doe',
           email: 'john.doe@lukkon.com',
           address: 'Chicago, brains 0' + i
         });
       }
     },
     paginData(data){
       this.paginEntries = data
     }
    
   }
   
 });

*/


export default {
name: 'paginator',
props: {
  entries: {type: Array},
  perPage: {type: Number, default: 10},
  color: {type: String, default: '#28B1E4'}
},
data(){
  return {
    currentPage: 1,
    
  };
},
computed: {
  paginStyle () {
    return {
        display: 'flex',
        justifyContent: 'flex-end',
        color: this.color
    }
  },
  btnStyle(){
    return {
     border: '1px solid '+ this.color,
      outline: 'none',
      padding: '5px 10px',
      borderRadius: '3px',
      margin: '5px',
      color: this.color,
      background: '#fff',
    }
  },
  btnSelStyle(){
    return {
      color: '#fff',
      background: this.color
    }
  },
  pages(){
    var page = []
     for(let p=1; p<= Math.ceil(this.entries.length/this.perPage); p++){
       page.push(p)
     }
     this.$emit('data-changed', this.paginatedDatas)
     return page;
  },
  paginatedDatas(){
     return this.paginate(this.entries)
  }
},
methods:{
  prev(){
    if(this.currentPage > 1){
      this.currentPage--
    }
  },
  next(){
    if(this.currentPage < this.pages.length){
       this.currentPage++
    }
  },
  paginate(datas){
    let from = (this.currentPage*this.perPage) - this.perPage
    let to = this.currentPage * this.perPage
    return datas.slice(from, to)
  }
}
 
}

</script>

<template>
 <div class="paginator" :style="paginStyle">
        <button class="btn" :style="btnStyle" @click.prevent="prev">&lt;&lt;</button>
        <div v-if="currentPage>3">
          <button class="btn" :style="[btnStyle, currentPage==1 ? btnSelStyle : '' ]"
          @click.prevent="currentPage=1" 
              >{{ '1' }}</button>
          <span>...</span>
        </div>
        <button class="btn" v-for="p in pages.slice(currentPage-1,currentPage+2)" :key="p"
        @click.prevent="currentPage=p" 
        :style="[btnStyle, p==currentPage ? btnSelStyle : '' ]">
        {{ p }}
        </button>
        <div v-if="(currentPage+5)<pages.length">
          <span>...</span>
          <button class="btn" :style="[btnStyle, currentPage==pages.length ? btnSelStyle : '' ]" 
          @click.prevent="currentPage=pages.length"
            >{{ pages.length }}</button>
        </div>
        <button class="btn" :style="btnStyle" @click.prevent="next">&gt;&gt;</button>
    </div>  
</template>
