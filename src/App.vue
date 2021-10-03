<template>
  <div class="container column">
     <app-form 
     @push="push"
     >
     </app-form>
       
       
      <div v-if="!!options.length" class="card card-w70">
       <component  v-for="(option,index) in options" :key="index" :is="'App' + option.type"
       v-html="option.value"
       ></component>
    </div>
    <div  v-else class="card card-w70">
      <h3>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
   
  </div>
   
   <app-loader v-if="loader"></app-loader>
    
 <div v-else  class="container">
    <p>
      <button  @click="get" class="btn primary">{{btnText}}</button>
    </p>
      <div>
    <div v-if="show" class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li v-for="(person,index) in people" :key="index" class="list-item">
          <div>
            <p><strong>{{person.email}}</strong></p>
            <small>{{person.name}}</small>
          </div>
        </li>
      </ul>
    </div>
    </div>
    <div v-if="loader" class="loader" ></div>
  </div>

</template>

<script>
import AppForm from './AppForm.vue'
import Apptitle from  './AppTitle.vue'
import Appavatar from './AppAvatar.vue'
import Appsubtitle from './AppSubtitle.vue'
import Apptext from './AppText.vue'
import axios from 'axios'
import AppLoader from './AppLoader.vue'



export default {
   components:{AppForm,Apptitle,Appavatar,Appsubtitle,Apptext,AppLoader},

   data(){
     return{
       options:[],
       show: false,
       loader: false,
       people:[],
       
       
     }
   },
   methods:{
     push(data){
      this.options.push(data)
      console.log(this.options[0].value)
     },

    
 async get(){
    this.loader=true
   const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
  const result = Object.keys(data).map(key=>{
     return{
       id:key,
       name:data[key].name,
       email:data[key].email
     }
     
   })

   this.loader=false
   
    this.people=result
    
    

    this.show=!this.show
    
     }
   },
  
   computed:{
     btnText(){
         if(this.show){
      return 'Скрыть комментарии'
    }else{
      return 'Загрузить комментарии'
    }

     }
   }


}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
