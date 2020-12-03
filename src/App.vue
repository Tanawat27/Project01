<template>
  <div id="app">
    <Kanban :data="data"/>
  </div>
</template>

<script>
import Kanban from "./components/Kanban.vue";

export default {
  name: "App",
  components: {
    Kanban,
  },
  data() {
    return {
      data: [
        {
          name: "todo",
          color: "#F000FF",
          task:[]
        },
        {
          name: "doing",
          color: "#E7B563",
          task:[]
        },
        {
          name: "done",
          color: "#70D47A",
          task:[]
        },
      ],
    };
  },
};
</script>

<style>
#app {
  height: 100vh;
}
</style>
