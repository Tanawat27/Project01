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
        <div class="createtask" @click="createtask(index)">Create Task</div>
      </div>
    </div>
    <b-modal ref="createtaskmodal" title="Create Task">
    <p class="my-4">Hello from modal!</p>
  </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    data: Array,
  },
  methods:{ 
      createtask(indec_column){
          console.log(indec_column);
          this.$refs["createtaskmodal"].show()
      }
      }
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
.createtask:hover{
    background-color: rgb(3, 73, 204);
}
</style>