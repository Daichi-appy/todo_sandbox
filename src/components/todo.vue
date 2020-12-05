<template>
  <div id="app" class="container">
    <h1>
      <button @click="parge">Parge</button>
      MyTodos
      <span class="info">({{ remaining.length }} / {{ todos.length }})</span>
    </h1>
    <ul v-if="todos.length">
      <li v-for="(todo, index) in todos">
        <input type="checkbox" v-model="todo.isDone" />
        <span :class="{ done: todo.isDone }">{{ todo.title }}</span>
        <span @click="deleteItem(index)" class="command">[x]</span>
      </li>
      <li v-show="!todos.length">Nothing to do, yay!</li>
    </ul>
    <ul v-else>
      <li>Nothing to do, yay!</li>
    </ul>
    <form @submit.prevent="addItem">
      <input type="text" v-model="newItem" />
      <input type="submit" value="Add" class="command" />
    </form>
  </div>
</template>
<script>
export default {
  data: function () {
    return {
      newItem: "",
      todos: [],
    };
  },
  watch: {
    todos: {
      handler: function () {
        localStorage.setItem("todos", JSON.stringify(this.todos));
        // alert('Data saved!');
      },
      deep: true,
    },
  },
  methods: {
    addItem: function () {
      var item = {
        title: this.newItem,
        isDone: false,
      };
      this.todos.push(item);
      this.newItem = "";
    },
    deleteItem: function (index) {
      this.todos.splice(index, 1);
    },
    parge: function () {
      if (!confirm("delete finished?")) {
        return;
      }
      this.todos = this.remaining;
    },
  },
  mounted: function () {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
  },
  computed: {
    remaining: function () {
      return this.todos.filter(function (todo) {
        return !todo.isDone;
      });
    },
  },
};
</script>

<style scoped>
.container {
  width: 300px;
  margin: auto;
}

#app h1 {
  font-size: 16px;
  border-bottom: 1px solid #ddd;
  padding: 16px 0;
}

#app li {
  line-height: 1.5;
}

#app input[type="text"] {
  padding: 2px;
}

#app input[type="submit"] {
  font-size: 13px;
  margin-left: 3px;
}

.command {
  font-size: 12px;
  cursor: pointer;
  color: #08c;
}

#app ul {
  padding: 0px;
  list-style: none;
}

#app li > span.done {
  text-decoration: line-through;
  color: #bbb;
}

.info {
  color: #bbb;
  font-size: 12px;
  font-weight: normal;
}

#app h1 > button {
  float: right;
}
</style>