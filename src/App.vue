<template>
  <div id="app">
    <h4 class="bg-primary text-white text-center p-2">{{ name }}'s To Do List</h4>
    <div class="container-fluid p-4">
      <!-- adding a little bit more features to enable the deletion of completed tasks and the ability to display a message when there are no more tasks to be completed  -->
      <div class="row" v-if="filteredTasks.length == 0">
        <div class="col text-center">
          <b>Nothing to do. Hurray!</b>
        </div>
      </div>
      <template v-else>
        <div class="row">
          <div class="col fw-bold">Task</div>
          <div class="col-3 fw-bold text-center">Done</div>
        </div>
        <!-- 2nd feature adding a filtering effect to rearrange the list each time a task is checked completed-->
        <div class="row" v-for="t in filteredTasks" v-bind:key="t.action">
          <div class="col">{{ t.action }}</div>
          <div class="col-3 text-center">
            <!-- 1st feature adding a check box for easy responding useability -->
            <input type="checkbox" v-model="t.done" class="form-check-input" />{{
              t.done
            }}
          </div>
        </div>
      </template>
      <!-- 3rd feature adding a create option button to add a new task  -->
      <div class="row py-2">
        <div class="col">
          <input v-model="newItemText" type="form-control" />
        </div>
        <div class="col-3 text-center">
          <button class="btn btn-primary" v-on:click="addNewTodo">Add</button>
        </div>
      </div>
      <div class="row bg-secondary py-2 mt-2 text-white">
        <div class="col text-center">
          <input v-model="hideCompleted" type="checkbox" class="form-check-input" />
          <label class="form-check-label fw-bold"> Hide completed tasks </label>
        </div>
        <div class="col text-center">
          <button class="btn btn-sm btn-warning" v-on:click="deleteCompleted">
            Delete Completed
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  // adding a 4th feature to enable this app create, store and retrive its stored data locally on the browser
  data() {
    return {
      name: "Ugo",
      tasks: [],
      hideCompleted: true,
      newItemText: "",
    };
  },
  computed: {
    filteredTasks() {
      return this.hideCompleted ? this.tasks.filter((t) => !t.done) : this.tasks;
    },
  },
  methods: {
    addNewTodo() {
      this.tasks.push({
        action: this.newItemText,
        done: false,
      });
      localStorage.setItem("todos", JSON.stringify(this.tasks));
      this.storeData();
      this.newItemText = "";
    },
    storeData() {
      localStorage.setItem("todos", JSON.stringify(this.tasks));
    },
    deleteCompleted() {
      this.tasks = this.tasks.filter((t) => !t.done);
      this.storeData();
    },
  },
  created() {
    let data = localStorage.getItem("todos");
    if (data != null) {
      this.tasks = JSON.parse(data);
    }
  },
};
</script>
