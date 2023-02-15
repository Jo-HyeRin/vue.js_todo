<template>
  <div class="inputBox shadow">
    <!-- v-on:keyup.enter="addTodo 엔터 누르면 실행되게 하기 -->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
        <i class="fas fa-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
    data: function() {
        return {
            newTodoItem: ""
        }
    },
    methods: {
        addTodo: function() {
            if(this.newTodoItem !== ''){
                var obj = {completed: false, item: this.newTodoItem};
                // console.log(this.newTodoItem);
                // localStorage에 저장하는 로직 = localStorage.setItem(키, 밸류);
                // localStorage.setItem(this.newTodoItem, obj); // value obj 객체 내부에 어떤 값이 있는 지 알 수 없다.
                localStorage.setItem(this.newTodoItem, JSON.stringify(obj));
                // 값 비우는 로직
                this.clearInput();
            }
        },
        clearInput: function() {
            this.newTodoItem = '';
        }
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478fb, #8763fb);
    display: block;
    width: 3rem;
    border-radius:0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
</style>