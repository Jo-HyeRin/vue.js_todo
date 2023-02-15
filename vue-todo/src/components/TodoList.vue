<template>
  <div>
    <ul>
        <li v-for="todoItem in todoItems" v-bind:key="todoItem">
            {{ todoItem }}
        </li>
    </ul>
  </div>
</template>

<script>
export default {
    data: function() {
        return {
            todoItems: []
        }
    },
    created: function() {
        // 로컬스토리지 값 가져우기
        if(localStorage.length > 0) {
            for(var i = 0; i < localStorage.length ; i++) {
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    // 로컬스토리지 값 확인하기 : console.log(localStorage.key(i));
                    this.todoItems.push(localStorage.key(i));                
                }
            }
        }
    }
}
</script>

<style>

</style>