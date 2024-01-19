<template>
<div>
<li>
    <label>
        <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)"/>
        <span v-show="!todo.isEdit">{{todo.title}}</span>
        <input ref="inputTitle" v-show="todo.isEdit"  type="text" :value="todo.title" @blur="handleBlur(todo,$event)"/>
    </label>
    <button class="btn btn-edit" @click="handleEdit(todo)">编辑</button>
    <button class="btn btn-danger" @click="deleteHand(todo)">删除</button>
    
</li>
</div>
</template>
<script>
export default{
    name:"MyItem",
    props:['todo','checkTodo','deleteTodo','updateTodo'],
    methods:{
      handleCheck(id){
        this.checkTodo(id)
      },
      deleteHand(id){
        this.deleteTodo(id)
      },
      handleEdit(todo){
    if(todo.hasOwnProperty.call('isEdit')){
      todo.isEdit=true
    }else{
      this.$set(todo,'isEdit',true)
    }
    this.$nextTick(function(){
      this.$refs.inputTitle.focus()
    })
  },
      handleBlur(todo,e){
        todo.isEdit = false
        
        this.updateTodo(todo.id,e.target.value)
      }
    }
}
</script>
<style scoped>
/*item*/
.btn-edit{
  color: #fff;
  background-color: skyblue;
  border:1px solid rgb(103, 159, 180);
  margin-left: 5px;
}
li:hover{
  background-color: #ddd;
}
 li{
  
  
  list-style: none;
  height:36px;
  line-height:36px;
  padding:0 5px;
  border-bottom:1px solid #ddd;
 }
 label{
  float: left;
  cursor:pointer;
 }

 input{
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top:-1px;
 }
li button{
  float: right;
  display: none;
  margin-top:3px;
 }
 li:before{
  content:initial;
 }
 li:last-child{
  border-bottom:none;
 }
 li:hover button{
  display: block;
}
</style>