<template>
    <div class="datable">
            <table class="table">
            <thead >
            <tr>
              <th v-for="h in dataHeaders" :key="h" v-html="h"></th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="item in mergeDatas" :key="item">
                <td>{{ item.id }}</td>
                <td>{{ item.name }}</td>
                <td>{{ item.email}}</td>
                <td>{{ item.address }}</td>
                <td></td>
            </tr>
            </tbody>
            </table>
            <!-- pagination -->
            <div class="paginator" :style="paginStyle"  v-if="isPaginable">
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

         </div>
</template>
<script>
export default {
     props: {
        dataHeaders: {type: Array, required: true},
        dataEntries: {type: Array, required: true},
        perPage: {type: Number, default: 10},
        isPaginable: {type: Boolean, default: true},
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
        for(let p=1; p<= Math.ceil(this.dataEntries.length/this.perPage); p++){
          console.log(p)
          page.push(p)
        }
        return page;
     },
     mergeDatas(){
       return this.isPaginable ? this.paginate(this.dataEntries) : this.dataEntries
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
       console.log(this.currentPage+'/'+this.perPage)
       console.log(datas.length)
       let from = (this.currentPage*this.perPage) - this.perPage
       let to = this.currentPage * this.perPage
       return datas.slice(from, to)
     }
   }
}
</script>
