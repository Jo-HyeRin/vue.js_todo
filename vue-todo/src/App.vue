<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <!-- <TodoInput v-on:하위컴포넌트에서 발생시킨 이벤트 이름="현재컴포넌트의 메서드정의"></TodoInput> -->
    <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
    <!-- <TodoList v-bind:내려보낼프롭스속성이름="현재위치컴포넌트데이터속성"></TodoList> -->
    <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem"></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  methods: {
    addOneItem: function(todoItem) {
      var obj = {completed: false, item: todoItem};
      // localStorage에 저장하는 로직 = localStorage.setItem(키, 밸류);
      // localStorage.setItem(this.newTodoItem, obj); // value obj 객체 내부에 어떤 값이 있는 지 알 수 없다.
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index) {
      console.log(todoItem);
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1); // index, 삭제할개수
    }
  },
  created: function() {
    // 로컬스토리지 값 가져우기
    if(localStorage.length > 0) {
        for(var i = 0; i < localStorage.length ; i++) {
            if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                // 로컬스토리지 값 확인하기 : console.log(JSON.parse(localStorage.getItem(localStorage.key(i)))); 
                this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));             
            }
        }
    }
  },
  components: {
    // 컴포넌트 태그명 : 컴포넌트 내용
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f6;
}
input {
  border-style: groove;
  width: 200px;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>