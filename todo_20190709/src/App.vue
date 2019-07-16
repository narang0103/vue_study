<template>
  <div id="app">
    <div class="container--tabs">
      <div class="col-md-6 offset-md-3">
        <h1 class="text-center mb-4">Todo List</h1>
        <input type="text" class="form-control mb-4" v-model="userInput" @keyup.enter="addNewTodo">

        <div class="list-group mb-4">
          <v-tabs
                  background-color="transparent"
                  color="basil"
                  grow
                  >
            <v-tab
                    v-for="(tab, index) in tabs"
                    :key="index"
                    @click="changeCurrentState(tab.value)"
                    >{{tab.name}}
            </v-tab>
          </v-tabs>
        </div>
        <div class="list-group mb-4 tab-pane fade show active" id="tab-content">
          <template v-for="todo in actionTodoList">
            <button type="button" class="list-group-item text-left" @click="toggleState(todo)">{{todo.label}}</button>
          </template>
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
        tabs : [{
          name:'할일',
          value:'active'
        },{
          name:'완료',
          value:'done'
        },{
          name : '전체',
          value:'all'
        }]
      }
    },
    computed : {

      actionTodoList(){
        return this.todo.filter(todo => todo.state === this.currentState || this.currentState === 'all');
      }

    },
    methods : {
      addNewTodo(){
        if (this.userInput.length > 0) {
          this.todo.push({
            label : this.userInput,
            state : 'active',
          });
          this.userInput = '';
        }
      },
      changeCurrentState(state){
        this.currentState = state;
      },
      toggleState(todo){
        todo.state = todo.state === 'active'?'done':'active';
      }
    }
  };
</script>
<style>
  /*
  #app {
    font-family:'Avenir', Helvetica, Arial, sans-serif;
    text-align:center;
    color:#2c3e50;
    margin-top:30px;
  }
  */

</style>