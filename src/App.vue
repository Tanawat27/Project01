<template>
  <div id="app">
    <Kanban :data="data" :create_task_submit ="create_task_submit"/>
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
          tasks:[{
            task_name:"tast"
          }]
        },
        {
          name: "doing",
          color: "#E7B563",
          tasks:[{
            task_name:"tast"
          }]
        },
        {
          name: "done",
          color: "#70D47A",
          tasks:[{
            task_name:"tast"
          }]
        },
      ],
    };
  },
  methods:{
    create_task_submit(column_index,item){
      this.data[column_index].tasks.push(item)
    }
  }
};
</script>

<style>
#app {
  height: 100vh;
}
</style>
