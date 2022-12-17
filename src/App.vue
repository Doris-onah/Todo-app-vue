<template>
  <div class="vue">
  <div class="app">
   
    <div class="app-con">
      <h1>Todo App</h1>
      <div class="name">
        <h2>
          Hello,<input
            type="text"
            placeholder="Enter Your Name"
            v-model="name"
            class="name-box"
          />
        </h2>
      </div>

      <div>
        <h3>what's on your todo list?</h3>
        <div class="todo">
        <input type="text"
         v-model="newTodo" 
         placeholder="ENTER YOUR TODO HERE"
         class="new-todo" />
         </div>
<br/>

<div class="add-todo-btn">
        <button @click="addTodo"
         class="add-todo">Add Todo</button>
         </div>
      </div>
<br/>

      <div class="todo-container">
      <div v-for="(todos, i) in todo" 
      :key="i" class="todo-item">

        <div class="todos">🖤 {{ todos }} </div>
       <div> <button @click="deleteTodo(i)" class="delete-btn">delete</button></div>
      </div>
      </div>
    </div>

  </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: " ",
      todo: [],
      newTodo: "",
    };
  },

  watch: {
    name() {
      localStorage.setItem("name", this.name);
    },
   todo : {
     handler() {
       localStorage.setItem("todo", JSON.stringify(this.todo));
     },
     deep: true,
   },
   
},


  methods: {
    setTodos(todo) {
      localStorage.setItem("todo", JSON.stringify(todo));
    },
    getTodos() {
      const storedTodos = localStorage.getItem("todo");

      if (storedTodos) {
        return JSON.parse(storedTodos);
      }

      return [];
    },
    addTodo() {
        
        if (this.newTodo.length < 5)
        {
            alert("Todo must be at least 4 characters long");
            this.newTodo = "";
        }
        else
        {
            this.todo.push(this.newTodo);
            this.newTodo = "";
        }
        
          },

     

    deleteTodo(i) {
      this.todo.splice(i, 1);
    },
  },


  mounted() {
    this.name = localStorage.getItem("name");
  this.todo = this.getTodos();
  },
};
</script>
<style>

.vue {
max-height: 100%;
display: flex;
  justify-content: center;
  align-items: center;
  max-width: 100%;
}
.app {
  width: 30%;
  max-height: fit-content;
  height: 100%;
  background-color: rgb(240, 245, 240);
  box-shadow: rgb(112, 111, 111) 3px 2px 3px 4px;
 display: flex;
 justify-content: center;
 align-items: center;
 border: 15px solid rgb(240, 245, 240);
 border-radius: 30px;
}

.app-con {
  display: block;
  justify-content: center;
  align-items: center;
  width: 500px;
  height: 100%;
  border-radius: 10px;
  box-shadow: rgb(112, 111, 111) 3px 3px 5px 4px;
  background-color: white;
  border: 8px  solid white;
}
.name {
  align-items: center;
  background-color: rgb(156, 195, 210);
  display: flex;
  justify-content: center;
}
.name-box {
  all: unset;
  text-align: start;
  width: 60%;
  text-transform: capitalize;
 background-color: rgb(156, 195, 210);;
}

.todo-container {
  
  width: 100%;
  height: 80%;
  height: fit-content;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 15px;
}
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 90%;
  height: 90%;
  margin: 10px 0;
  gap: 10px;
}
.todo {
  align-items: center;
  text-align: center;
}
.todos {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  border-radius: 5px;
}
.add-todo {
  background-color: rgb(24, 120, 24);
  border-radius: 10px;
  height: 30px;
  border: none;
  color: black;
  box-shadow: rgb(5, 56, 5) 1px 2px 3px 4px;
  

}
.add-todo-btn {
  display: flex;
  justify-content: center;
  align-items: center;
}
.delete-btn {
  border: none;
  width: 30px;
  width: 60px;
  color: black;
  box-shadow: 1px 2px 3px 4px rgba(20,20,20,0.4);
}
h1 {
  align-items: center;
  text-align: center;
}
.new-todo {
  width: 90%;
  height: 40px;
  border-radius: 10px;
  background-color: rgb(251, 250, 251);
}
@media screen and (max-width: 768px) {
  .app {
    width: 100%;
  }
  .app-con {
    width: 100%;
  }
  .name-box {
    width: 80%;
  }
  .todo-item {
    width: 90%;
  }
  .new-todo {
    width: 80%;
  }
}


</style>
