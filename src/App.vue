<template>
  
  <div class="app">
    <h1>List Kunjungan Wisata</h1>
    <div class="add-todo">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Tambahkan tempat wisata">
      <button @click="addTodo">Tambah</button>
    </div>
    <div class="filters">
      <label>
        <input type="checkbox" v-model="showIncomplete"> Tampilkan tempat yang belum di kunjungi
      </label>
    </div>
    <ul class="todos">
      <li v-for="(todo, index) in filteredTodos" :key="index" :class="{ 'completed': todo.completed }">
        <input type="checkbox" v-model="todo.completed">
        <span v-if="!todo.editing" @click="toggleCompletion(todo)" :class="{ 'completed-text': todo.completed }">{{ todo.text }}</span>
        <input v-else type="text" v-model="todo.text" @keyup.enter="stopEditing(todo)">
        <button @click="removeTodo(index)">Hapus</button>
        <button @click="editOrSave(todo)">{{ todo.editing ? 'Simpan' : 'Edit' }}</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ListKunjunganWisata',
  data() {
    return {
      newTodo: '',
      showIncomplete: false,
      todos: []
    };
  },
  computed: {
    filteredTodos() {
      if (this.showIncomplete) {
        return this.todos.filter(todo => !todo.completed);
      } else {
        return this.todos;
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, completed: false, editing: false });
        this.newTodo = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    toggleCompletion(todo) {
      todo.completed = !todo.completed;
    },
    editOrSave(todo) {
      if (todo.editing) {
        todo.editing = false;
      } else {
        todo.editing = true;
      }
    },
    stopEditing(todo) {
      todo.editing = false;
    }
  }
};
</script>

<style scoped>
body {
  color: #333;
}
.app {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #171515;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  color: #333;
}

.add-todo {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.add-todo input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 70%;
  margin-right: 10px;
}

.add-todo button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-todo button:hover {
  background-color: #0056b3;
}

.filters {
  text-align: center;
  margin-bottom: 20px;
}

.filters label {
  font-size: 16px;
}

.todos {
  list-style-type: none;
  padding: 0;
}

.todos li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ccc;
  transition: background-color 0.3s;
}

.todos li:hover {
  background-color: #f1f1f1;
}

.todos li .completed-text {
  text-decoration: line-through;
  color: #888;
}

.todos li input[type="text"] {
  flex: 1;
  margin-right: 10px;
  padding: 5px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.todos li button {
  margin-left: 10px;
  padding: 5px 10px;
  font-size: 14px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.todos li button:nth-child(3) {
  background-color: #28a745;
  color: white;
}

.todos li button:nth-child(3):hover {
  background-color: #218838;
}

.todos li button:nth-child(4) {
  background-color: #dc3545;
  color: white;
}

.todos li button:nth-child(4):hover {
  background-color: #c82333;
}
</style>
