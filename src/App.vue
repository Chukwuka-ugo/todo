<template>
  <div id="app">
    <h4 class="bg-primary text-white text-center p-2">
      {{ name }}'s To Do List
    </h4>
    <div class="container-fluid">
      <div class="row">
        <div class="col fw-bold">Task</div>
        <div class="col-2 fw-bold">Done</div>
      </div>
      <!-- 2nd feature adding a filtering effect to rearrange the list each time a task is checked completed-->
      <div class="row" v-for="t in filteredTasks" v-bind:key="t.action">
        <div class="col">{{ t.action }}</div>
        <div class="col-2 text-center">
          <!-- 1st feature adding a check box for easy responding useability -->
          <input type="checkbox" v-model="t.done" class="form-check-input" />{{ t.done }}
        </div>
      </div>
      <div class="row bg-secondary py-2 mt-2 text-white">
        <div class="col text-center">
          <input v-model="hideCompleted" type="checkbox" class="form-check-input" />
          <label class="form-check-label fw-bold">
            Hide completed tasks
          </label>
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
      name: "Ugo",
      tasks: [{ action: "Buy Flowers", done: false },
      { action: "Get Shoes", done: false },
      { action: "Collect Tickets", done: true },
      { action: "Call Ade", done: false }],
      hideCompleted: true
    };
  },
  computed:{
    filteredTasks(){
      return this.hideCompleted ?
      this.tasks.filter(t => !t.done) : this.tasks
    }
  }
};
</script>
