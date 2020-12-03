<template>
  <div class="AA">
    <div
      class="column"
      :style="{ backgroundColor: column.color }"
      v-for="(column, index) in data"
      :key="index"
    >
      <div class="columnheader">
        {{ column.name }}
      </div>
      <div class="columnbody">
        <div v-for="(task, task_index) in column.tasks" :key="task_index">
          <div
            class="task"
            :draggable="true"
            @dragstart="start_move(task_index, index)"
          >
            {{ task.task_name }}
          </div>
          <div
            class="drop_zone"
            @dragenter.prevent="drop_zone_enter"
            @dragleave.prevent="drop_zone_leave"
            @dragover.prevent
            @drop="drop_item(index, task_index)"
          ></div>
        </div>

        <div class="createtask" @click="createtask(index)">Create Task</div>
      </div>
    </div>
    <b-modal ref="createtaskmodal" title="Create Task">
      <input
        class="input-taskname"
        v-model="task_name"
        @keyup.13="submit_create_task"
      />
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    data: Array,
    create_task_submit: Function,
    move_item_task: Function,
  },
  methods: {
    createtask(index_column) {
      this.current_column_index = index_column;
      this.$refs["createtaskmodal"].show();
    },
    submit_create_task() {
      this.create_task_submit(this.current_column_index, {
        task_name: this.task_name,
      });
    },
    start_move(task_index, column_index) {
      this.current_column_index = column_index;
      this.current_task_index = task_index;
    },
    drop_zone_enter(event) {
      event.target.style.height = "100px";
      event.target.style.borderStyle = "dotted";
      event.target.style.transition = "height 0.5s";
    },
    drop_zone_leave(event) {
      event.target.style.height = "10px";
      event.target.style.borderStyle = "none";
      event.target.style.transition = "height 0.5s";
    },
    drop_item(column_index, task_index) {
    
      
      this.move_item_task(
        this.current_column_index,
        this.current_task_index,
        column_index,
        task_index
      );
    },
  },
  data() {
    return {
      task_name: "",
      current_column_index: "",
      current_task_index: "",
    };
  },
};
</script>

<style>
.AA {
  width: 100%;
  height: 100%;
  background-color: rgb(148, 145, 145);
}
.column {
  height: 600px;
  width: 300px;
  border-radius: 20px;
  display: inline-block;
  /* margin-left: 50px;
  margin-top: 30px; */
  margin: 70px;
  -webkit-box-shadow: 11px 20px 24px 10px rgba(212, 127, 212, 1);
  -moz-box-shadow: 11px 20px 24px 10px rgba(212, 127, 212, 1);
  box-shadow: 11px 20px 24px 10px rgba(212, 127, 212, 1);
  padding: 20px;
}
.columnheader {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
  font-size: 32px;
  font-weight: bold;
}
.columnbody {
  height: calc(100% - 50px);
  background-color: rgba(241, 241, 241, 0.521);
  border-radius: 30px;
  padding: 5px;
}
.createtask {
  width: 100%;
  height: auto;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
}
.createtask:hover {
  background-color: rgb(3, 73, 204);
}
.input-taskname {
  width: 100%;
}
.task {
  width: auto;
  height: 100px;
  position: relative;
  border-radius: 2px;
  margin: 10px;
  background-color: rgb(184, 184, 184);
}
.drop_zone {
  height: 10px;
}
</style>