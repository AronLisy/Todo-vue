<template>
  <div id="content">
    <div class="wrapper">
      <div
        class="task"
        v-for="(todo, index) in todos"
        v-bind:key="todo.id">
        <div>
          {{ todo.title }}
        </div>
        <button v-on:click="removeTodo(index)">done</button>
      </div>
      <div id="template">
        <form id="newTask" v-on:submit.prevent="addNewTodo">
          <input id="taskInput"
            type="text"
            placeholder="Enter task..."
            v-model="newTodo">
          <input type="submit" value="save" id="saveBtn">
        </form>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      newTodo: '',

      todos: [{
        id: 1,
        title: 'learn Vue.js'
      }, {
        id: 2,
        title: 'create a project'
      }],

      nextTodoId: 3
    }
  },
  methods: {
    addNewTodo: function() {
      if (this.newTodo === ""){
        return;
      }
        else {
          this.todos.push({
              id: this.nextTodoId++,
              title: this.newTodo
          })
        }
        this.newTodo =''
    },

    removeTodo: function(index) {
      this.todos.splice(index, 1);
    }
  }
}

</script>

<style scoped>
#template {
  display: block;
  padding: 1px 25px;
  border: solid #594A54 2px;
  border-radius: 15px;
  background-color: #C2CEC6;
  height: 38px;
  margin: 0px auto 50px auto;
  align-items: center;
  justify-content: space-between;
}

#taskInput {
  width: 85%;
  border: 0px;
  background-color: #C2CEC6;
  height: 26px;
  margin-top: 3px;
  float: left;
}
#taskInput:focus {
  outline: none;
}

#saveBtn {
  background-color: #C2CEC6;
  border: 0px;
  border-radius: 5px;
  width: 15%;
  height: 26px;
  margin-top: 3px;
  padding: 0px 0px;
  color: #594A54;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 14px;
  float: left;
}
#saveBtn:hover {
  background-color: #6FA198;
  transition: linear 0.2s;
  cursor: pointer;
}
#tsaveBtn:focus {
  outline: none;
}

.wrapper {
  margin: auto;
  width: 80%;
}

.task {
  padding: 5px 25px 5px 25px;
  border: solid #594A54 2px;
  border-radius: 15px;
  background-color: #C2CEC6;
  min-height: 38px;
  margin: 0px 0px 12px 0px;
  text-align: left;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task button {
  background-color: #C2CEC6;
  border: 0px;
  border-radius: 5px;
  width: 15%;
  height: 26px;
  margin-top: -1px;
  padding: 0px 0px;
  color: #594A54;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 14px;
  float: left;
}
.task button:hover {
  background-color: #C46666;
  transition: linear 0.2s;
  cursor: pointer;
}
.task :focus {
  outline: none;
}

</style>
