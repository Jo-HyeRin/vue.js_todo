<template>
  <div class="inputBox shadow">
    <!-- v-on:keyup.enter="addTodo 엔터 누르면 실행되게 하기 -->
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <!-- <button v-on:click="addTodo">add</button> -->
    <span class="addContainer" v-on:click="addTodo">
        <i class="fas fa-plus addBtn"></i>
    </span>

    <button id="show-modal" @click="showModal = true">Show Modal</button>

    <Teleport to="body">
    <!-- use the modal component, pass in the prop -->
    <modal :show="showModal" @close="showModal = false">
        <template #header>
        <h3>custom header</h3>
        </template>
    </modal>
    </Teleport>

  </div>
</template>

<script>
import Modal from './common/CommonModal.vue'

export default {
    data: function() {
        return {
            newTodoItem: "",
            showModal: false
        }
    },
    methods: {
        addTodo: function() {
            if(this.newTodoItem !== ''){
                this.$emit('addTodoItem', this.newTodoItem);
                // 값 비우는 로직
                this.clearInput();
            }
        },
        clearInput: function() {
            this.newTodoItem = '';
        }
    },
    components: {
        // TodoInput의 하위 컴포넌트 
        'modal': Modal
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