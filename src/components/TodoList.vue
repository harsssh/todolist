<template>
  <div>
    <h2>TODO List</h2>
    <label>
      タスク名
      <input type="text" v-model="newTaskName" />
    </label>
    <label>
      期限
      <input type="text" v-model="newTaskDeadline" />
    </label>
    <button @click="addTask">追加</button>
    <button @click="finishTask">完了</button>
    <div class="task">
      <div class="notDone">
        <h3>未完了</h3>
        <div v-for="(task, i) in currentTask" :key="i">
          <input type="checkbox" :id="i" :value="i" v-model="doneIndex" />
          <label :for="task.name"
            >{{ task.name }}: {{ task.deadline }}まで</label
          >
        </div>
      </div>
      <div class="done">
        <h3>完了</h3>
        <div v-for="task in doneTask" :key="task.name">
          {{ task }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      currentTask: [],
      doneTask: [],
      doneIndex: [],
      newTaskName: "",
      newTaskDeadline: ""
    };
  },
  methods: {
    addTask() {
      if (this.newTaskName === "" || this.newTaskDeadline === "") return;
      this.currentTask.push({
        name: this.newTaskName,
        deadline: this.newTaskDeadline
      });
    },
    finishTask() {
      for (let i = 0; i < this.doneIndex.length; i++) {
        this.doneTask.push(this.currentTask[this.doneIndex[i]].name);
        this.currentTask.splice(this.doneIndex[i], 1, "done");
        this.currentTask = this.currentTask.filter(function(ele) {
          return ele != "done";
        });
      }
    }
  }
};
</script>

<style scoped>
.task {
  width: 500px;
  margin-left: auto;
  margin-right: auto;
}
.notDone {
  width: 250px;
  float: left;
}
.done {
  width: 250px;
  float: left;
}
</style>
