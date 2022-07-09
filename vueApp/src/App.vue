<template>

    <div id="app">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
      <!-- v-on:removeTodo의 약식 = @removeTodo -->
      <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
    </div>

</template>

<script>
// src를 기준으로 상대좌표
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data(){
    return{
      todoItems : []
    }
  },
  created(){
    if(localStorage.length > 0){
      for(var i = 0; i < localStorage.length; i++){
          this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods : {
    addTodo(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
  // 현재 처럼만 components를 등록하면 올바로 인식을 할 수 없다.
  // 싱글 컴포넌트 체계(.vue파일 체계)에서는 특정 컴포넌트에서 다른 위치에 있는 컴포넌트의 내용을 불러올 때 아래 형식을 사용한다.
  // ex) import 불로온 파일의 내뇽이 담길 객체 from '불러올 파일 위치'
  components:{
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter,
  }
}
</script>

<style>
  body{text-align: center; background-color: #f6f6f8;} /* 애플리케이션 전체 배경색 꾸밈 */
  input{border-style: groove; width: 200px;}
  button{border-style: groove;}
  .shadow{box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)}
</style>
