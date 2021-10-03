 <template>
      <form class="card card-w30">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="type">
         <option value="title">Заголовок</option>
         <option value="subtitle">Подзаголовок</option>
         <option value="avatar">Аватар</option>
         <option value="text">Текст</option>
        </select>
      </div>
      <div class="form-control">
        <label for="value">Значение</label>
        <textarea v-model="content" id="value" rows="3"></textarea>
      </div>
      <button class="btn primary" @click.prevent="data" :disabled="content.length<=2">Добавить</button>
    </form> 
 </template>


<script>

export default{
  
  emits:['push'],
  
  data(){
    return{
      content:'',
      type:'title'
    }
  },
  methods:{
    data(){
      this.$emit('push', {
         type:this.type,
         value: this.content
       })
      this.content=''
      this.type= 'title'
    }
  }
 

}
</script>







