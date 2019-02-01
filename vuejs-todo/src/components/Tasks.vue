<template>
  <div id="content">
    <div class="row justify-content-center">
      <h3>What are your tasks for today?</h3>
      <div
        class="task col-12 col-sm-10 col-md-9 col-xl-8"
        v-for="(todo, index) in todos"
        v-bind:key="todo.id"
      >
        <div class="row justify-content-center">
          <div class="col-9 col-lg-10">
            {{ todo.title }}
          </div>
          <div class="col-3 col-lg-2">
            <button v-on:click="removeTodo(index)">done</button>
          </div>
        </div>
      </div>
      <div
        id="template"
        class="col-12 col-sm-10 col-md-9 col-xl-8"
        v-on:mouseover="mouseOn = true"
        v-on:mouseout="mouseOn = false"
        v-bind:style="{ opacity: templateVisibility}"
      >
        <form
          id="newTask"
          v-on:submit.prevent="addNewTodo"
          class="row justify-content-center"
        >
          <input
            id="taskInput"
            class="col-9 col-lg-10"
            type="text"
            placeholder="Enter task..."
            v-model="newTodo"
            v-on:focus="focus = true"
            v-on:blur="focus = false"
          >
          <div class="col-3 col-lg-2">
            <input
            id="saveBtn"
            type="submit" value="save"
            >
          </div>
        </form>
      </div>
    </div>
    <button class="primaryBtn" v-on:click="showInfo=!showInfo">INFO</button>
    <div v-show="showInfo">
      <p>Welcome to a task list. This is the main section of this page.</p>
      <p>Are you sometimes overwhelmed by everything you need to do? Write down every little task and after each one press SAVE button or enter.</p>
      <p>Once you copleted a task, simply click DONE button and the task will disappear from your life.</p>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      newTodo: '',

      todos: [
        {
          id: 1,
          title: 'Create new tasks'
        }
      ],

      nextTodoId: 2,

      mouseOn: false,
      focus: false,

      showInfo: false
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

  },

  computed: {
    templateVisibility: function() {
      if (this.mouseOn === false && this.focus === false) {
        return 0.4
      }
        else {
          return 1
        }
    }
  }

}

</script>

<style scoped>
#template {
  display: block;
  padding: 2px 28px;
  border: solid #594A54 2px;
  border-radius: 21px;
  background-color: #C2CEC6;
  min-height: 42px;
  margin: 0px auto;
  align-items: center;
  justify-content: space-between;
}
#template:hover {
  transition: 0.3s;
}

#taskInput {
  border: 0px;
  border-radius: 5px;
  background-color: #C2CEC6;
  height: 27px;
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
  height: 27px;
  margin-top: 3px;
  padding: 0px 5px;
  color: #594A54;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 14px;
  float: right;
  width: 50px;
}
#saveBtn:hover {
  background-color: #6FA198;
  transition: linear 0.2s;
}
#saveBtn:focus {
  outline: none;
}

.task {
  padding: 5px 28px;
  border: solid #594A54 2px;
  border-radius: 21px;
  background-color: #C2CEC6;
  min-height: 42px;
  margin: 0px 0px 8px 0px;
  text-align: left;
}

.task button {
  background-color: #C2CEC6;
  border: 0px;
  border-radius: 5px;
  height: 27px;
  padding: 0px 5px;
  color: #594A54;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 14px;
  float: right;
  width: 50px;
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
