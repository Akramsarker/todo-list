<template>
  <div class="container">
    <div id="main" class="card">
      <div class="card-content">
        <h1>Task List</h1>
        <form id="task-form">
          <div class="main-section" v-if="!isEditing">
            <div class="input-field">
              <input type="text" id="task" v-model="todo"/>
            </div>
            <div class="btn-center">
              <input
                type="submit"
                value="Add Task"
                class="btn"
                @click.prevent="storeTodo" 
              />
            </div>
          </div>
          <div class="main-section" v-else>
            <div class="input-field">
              <input type="text" id="task" v-model="todo" />
            </div>
            <div class="btn-center">
              <input
                type="submit"
                value="Update Task"
                class="btn"
                @click.prevent="upDateTodo"
              />
            </div>
          </div>
        </form>
      </div>
    </div>
    <div class="card-action">
      <div class="input-field">
        <input
          type="text"
          name="filter"
          id="filter"
          placeholder="Search Filter"
          v-model="filtersTodo"
        />
      </div>
      <h2>Tasks Add</h2>
      <ul class="collection">
        <li v-for="(todo, index) in filtersTodos" :key="todo">
          {{ todo }}
          <div class="icon">
            <i class="fas fa-pencil-alt" @click="editTodo(index, todo)"></i>
            <i class="fas fa-trash-alt icon-m" @click="deleteTodo(todo)"></i>
          </div>
        </li>
      </ul>
      <div class="btn-center btn-m">
        <a @click="clearFilds()" href="#" class="clear-tasks btn black"
          >Clear Tasks</a
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false,
      selectedIndex: null,
      todo: "",
      todos: ["Akram Sheikh", "Rabbi", "Nasim Uddin",'Nasir Uddin'],
      filtersTodo: "",
    };
  },
  methods: {
    storeTodo() {
      this.todos.push(this.todo);
      this.todo = "";
    },
    editTodo(index, todo) {
      this.todo = todo;
      this.selectedIndex = index;
      this.isEditing = true;
    },
    deleteTodo(index) {
      // this.todos.splice(index, 1);
      this.todos.splice(this.todos.indexOf(index), 1);
    },
    upDateTodo() {
      this.todos.splice(this.selectedIndex, 1, this.todo);
      this.isEditing = false;
      this.todo = "";
    },
    clearFilds() {
      this.todos.splice(0);
    },
    // showAlert() {
    //     // alert("Pleace Enter Your Todo List");
    //     console.log('Hello world')
    // },
  },
  computed: {
    filtersTodos() {
      return this.todos.filter((item) => {
        // return item.match(this.filtersTodo);
        return (
          item.toLowerCase().indexOf(this.filtersTodo.toLowerCase()) !== -1
        );
      });
    },
  },
};
</script>

<style scoped>
/* reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* container */
.container {
  max-width: 900px;
  margin: auto;
  padding: 0 10px;
}
h1 {
  text-align: center;
  padding: 1rem;
  font-size: 2.7rem;
  color: #616161;
  text-shadow: #e0e0e0 1px 1px 0;
}
h2 {
  text-align: center;
  padding: 1rem;
  font-size: 2rem;
  color: #616161;
  text-shadow: #e0e0e0 1px 1px 0;
}

li {
  display: flex;
  justify-content: space-between;
  list-style: none;
  margin: 9px 0px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 10px;
}
i {
  cursor: pointer;
}
i:hover {
  color: #5a5a5c;
}
.icon .icon-m {
  margin-left: 25px;
}
.collection-item {
  border: 1px solid #ccc;
  padding: 10px 16px 8px 16px;
  border-radius: 10px;
  margin-bottom: 10px;
  list-style: none;
  display: flex;
  justify-content: space-between;
}

.collection {
  max-width: 850px;
  margin: auto;
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 10px;
}

#main .card-content h1 {
  font-size: 3rem;
  padding: 2rem;
  text-align: center;
}

#task-title {
  font-size: 1.5rem;
  padding: 1.3rem;
  text-align: center;
}

/* input */
.input-field {
  text-align: center;
}

#task-form input[type="text"] {
  width: 80%;
  font-size: 16px;
  padding: 15px;
  border: 1px solid #ddd;
  margin-bottom: 7px;
  border-radius: 15px;
  outline: none;
}
#task-form input[type="text"]:hover {
  border: 1px solid #aaa;
}

.btn-center {
  text-align: center;
}

.btn-m {
  margin: 2rem;
}

/* submit btn */
input[type="submit"] {
  padding: 10px 1.5rem;
  font-size: 20px;
  border: 1px solid #aaa;
  border-radius: 10px;
  outline: none;
}

/* show alert */
.show-alert {
  margin: 2rem;
  padding: 10px;
  text-align: center;
  text-transform: capitalize;
  border-radius: 40px;
  color: #fff;
}

.success {
  background-color: green;
}

.error {
  background-color: red;
}

.btn {
  padding: 10px 1.5rem;
  background-color: #cccccc;
  color: #000;
  font-size: 20px;
  border: 1px solid #aaa;
  border-radius: 10px;
  outline: none;
  margin: 2rem;
  text-decoration: none;
  margin: 2rem;
  transition: 0.5s;
  cursor: pointer;
}

.btn:hover {
  background-color: #bbbbbb;
}
/* filter */
#filter {
  background-image: url("https://www.freeiconspng.com/thumbs/search-icon-png/search-icon-png-2.png");
  background-size: 21px 21px;
  background-position: 20px 15px;
  background-repeat: no-repeat;
  width: 80%;
  font-size: 16px;
  padding: 16px 30px 16px 55px;
  border: 1px solid #ddd;
  margin-bottom: 12px;
  border-radius: 100px;
  outline: none;
  transition: 0.5s;
}

#filter::placeholder {
  color: #9ea1a7;
}

#filter:hover {
  outline: none;
  box-shadow: 0 2px 7px 0 rgba(0, 0, 0, 0.2), 0 5px 16px 0 rgba(0, 0, 0, 0.2);
}
</style>
