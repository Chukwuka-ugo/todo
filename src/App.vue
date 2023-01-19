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
      <div class="row" v-for="t in tasks" v-bind:key="t.action">
        <div class="col">{{t.action}}</div>
        <div class="col-2">{{t.done}}</div>
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
      tasks:[{action:"Buy Flowers", done: false},
             {action:"Get Shoes", done: false},
             {action:"Collect Tickets", done: true},
             {action:"Call Ade", done: false}]
    };
  },
};
</script>
