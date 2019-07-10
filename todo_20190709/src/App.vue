<template>
  <div id="app">
    <div class="container">
      <div class="col-md-6 offset-md-3">
        <h1 class="text-center mb-4">Todo List</h1>
        <input type="text" class="form-control mb-4" v-model="userInput" @keyup.enter="addNewTodo">

        <div class="list-group mb-4">
          <ul class="nav nav-tabs">
            <li class="nav-item">
              <a class="nav-link active" data-toggle="tab" href="#" @click="changeCurrentState('active')">할일</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" data-toggle="tab" href="#" @click="changeCurrentState('done')">완료</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" data-toggle="tab" href="#" @click="changeCurrentState('all')">전체</a>
            </li>
          </ul>
        </div>



        <div class="list-group mb-4">
          <template v-for="todo in actionTodoList">
            <button type="button" class="list-group-item text-left" @click="toggleState(todo)">{{todo.label}}</button>
          </template>
        </div>

        <div class="text-right">
          <button type="button" class="btn btn-sm" @click="changeCurrentState('active')">할일</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState('done')">완료</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState('all')">전체</button>
        </div>

      </div>
    </div>
  </div>
</template>
<script>
  export default {
    name : 'app',
    data(){
      return {
        userInput : '',
        todo : [],
        currentState : 'active',
      }
    },
    computed : {

      actionTodoList(){
        return this.todo.filter(todo => todo.state === this.currentState || this.currentState === 'all');
      }

    },
    methods : {
      addNewTodo(){
        this.todo.push({
          label : this.userInput,
          state : 'active',
        });
        this.userInput = '';
      },
      changeCurrentState(state){
        this.currentState = state;
        return false;
      },
      toggleState(todo){
        todo.state = todo.state === 'active'?'done':'active';
      }
    }
  };
</script>
<style>
  #app {
    font-family:'Avenir', Helvetica, Arial, sans-serif;
    text-align:center;
    color:#2c3e50;
    margin-top:30px;
  }
</style>