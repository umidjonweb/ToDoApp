<template>
   <div class="todo-item" :class="{'todo--active':todo.completed}">
      <input type="checkbox" :checked="todo.completed" @change="oncheckbox"  >
      <input v-if="isedit" type="text" v-model="newtodoComment" @blur="diactive" ref="input"
       @keyup.esc="diactive" @keyup.enter="onchangecontent" >
      <div  v-else @dblclick="salom" class="sal"  >
        {{todo.content}}
      </div>
   </div>   
</template>

<script>
export default {
     name: 'TodoItem',
     props:['todo'],
   data() {
      return {
         newtodoComment:'',
         isedit:false
      };
   },

   methods: {
      oncheckbox(){
         this.$emit('xodisa');
      },
     onchangecontent(){
       this.$emit('edit',this.newtodoComment);
       this.isedit=false;
     },
      salom(){
       this.isedit=true;
        this.newtodoComment=this.todo.content; 
       
        this.$nextTick(()=>{
           this.$refs.input.focus(); 
        }) 
       },
       diactive(){
          this.isedit=false
       }
   },
};
</script>

<style lang="scss">
.todo-item{
   padding: 8px 4px;
   border-bottom: 1px solid #000;
   color: #4d4d4d;
   font-size: 24px;
   font-weight: normal;
   display: flex;
   align-items: center;
   input{
      font-size: inherit;
      color: inherit;
      border: none;
      outline: none;
      font-weight: normal;
   }
   .sal{
  flex-grow: 1;
   }
}
</style>