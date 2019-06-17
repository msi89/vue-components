<script>
/* 
 <datable 
          :data-headers="thead"
          :data-entries="datas" 
          :is-paginable="true"
          :pagin-color="paginatorColor"
        />
         data(){
     return {
       thead: ['Id', 'Name', 'Email', 'Address','<input type="checkbox" />'],
       datas: [],
       paginatorColor: '#00C384'
     };
   },
   mounted(){
    for(var i=1; i<=1000;i++){
         this.datas.push([
             i,'John Doe','john.doe@lukkon.com', 'Chicago, brains 0' + i
         ]);
       }
   },
*/
</script>

<template>
    <div class="datable">
      <div class="toolbar">
        <div class="filter">
          <select :style="styles.filter" v-model="linesPerPage">
            <option value="10">10</option>
            <option value="20">20</option>
            <option value="30">30</option>
            <option value="50">50</option>
            <option value="100">100</option>
          </select>
        </div>
        <div class="search">
          <input type="text" :style="styles.search" placeholder="search">
        </div>
      </div>
      <table class="table">
        <thead >
          <tr>
            <th v-for="h in dataHeaders" :key="h" v-html="h" :style="styles.header"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item,i) in mergeDatas" :key="i">
              <td v-for="(td,t) in item" :key="t">{{ td }}</td>
              <td></td>
          </tr>
        </tbody>
      </table>
            <!-- pagination -->
    <div class="paginator" :style="styles.paginator.default"  v-if="isPaginable">
      <button class="btn" :style="styles.paginator.button" @click.prevent="prev">&lt;&lt;</button>
      <div v-if="currentPage>3">
        <button class="btn" :style="[styles.paginator.button, currentPage==1 ? styles.paginator.buttonSelected : '' ]"
        @click.prevent="currentPage=1" 
            >{{ '1' }}</button>
        <span>...</span>
      </div>
      <button class="btn" v-for="p in pages.slice(currentPage-1,currentPage+2)" :key="p"
      @click.prevent="currentPage=p" 
      :style="[styles.paginator.button, p==currentPage ? styles.paginator.buttonSelected : '' ]">
      {{ p }}
      </button>
      <div v-if="(currentPage+5)<pages.length">
        <span>...</span>
        <button class="btn" :style="[styles.paginator.button, currentPage==pages.length ? styles.paginator.buttonSelected : '' ]" 
        @click.prevent="currentPage=pages.length"
          >{{ pages.length }}</button>
      </div>
      <button class="btn" :style="styles.paginator.button" @click.prevent="next" >&gt;&gt;</button>
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
        accentColor: {type: String, default: '#aaa'},
        headerTextColor: {type: String, default: '#555'},
        headerColor: {type: String, default: 'transparent'},
    },
    data(){
     return {
       currentPage: 1,
       linesPerPage: this.perPage
     };
    },
   computed: {
     styles() {
       return {
         header: {
           background: this.headerColor,
           color: this.headerTextColor,
         },
         paginator: {
            default: {
              display: 'flex',
              justifyContent: 'flex-end',
              color: this.accentColor
            },
            button:{
              cursor: 'pointer',
              border: '1px solid '+ this.accentColor,
              outline: 'none',
              padding: '5px 10px',
              borderRadius: '3px',
              margin: '5px',
              color: this.accentColor,
              background: '#fff', 
            },
            buttonSelected: {
              color: '#fff',
              background: this.accentColor
            },

            
         },
         filter: {
           border: '1px solid '+ this.accentColor,
           color:  this.accentColor
         },
         search: {
           border: '1px solid '+ this.accentColor,
           color:  this.accentColor
         }
       }
     },
     pages(){
       var page = []
        for(let p=1; p<= Math.ceil(this.dataEntries.length/this.linesPerPage); p++){
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
       let from = (this.currentPage*this.linesPerPage) - this.linesPerPage
       let to = this.currentPage * this.linesPerPage
       return datas.slice(from, to)
     }
   }
}

</script>
 <style>
 .datable .table{
  background: #fff;
  width: 100%;
  margin: 10px auto;
  border-collapse: collapse;
}
.datable .table th, td{
  text-align: left;
}

.datable .table th{
  padding: 10px 10px;
  border-bottom: 1px solid #ccc;
}
.datable .table td{
  padding: 5px 10px;
  border-bottom: 1px solid #f5f5f5;
}
.datable .btn-pagin-group{
  display: flex;
  justify-content: flex-end;
}
.datable .btn-pagin{
  background: #fff;
  border: 1px solid #ddd;
  color: #555;
  outline: none;
  padding: 5px 10px;
  border-radius: 3px;
  margin: 5px;
}
.datable .btn-pagin.selected{
  color: #444;
  background: #eee;
}
.datable .toolbar{
  display: flex;
  justify-content: space-between;
}
.datable .toolbar .filter select{
  outline: none;
  padding: 5px 10px;
  background: transparent;
  border-radius: 2px;
}.datable .toolbar .search input{
  outline: none;
  padding: 5px 10px;
  background: transparent;
  border-radius: 2px;
}
    </style>