<template>
  <div>
    <div>
      <h2>TodoList</h2>
    </div>
    <div>
      <label>
        Task
        <input type="text" v-model="newTaskName" />
      </label>
      <label>
        Deadline
        <input type="text" v-model="newTaskDeadline" />
      </label>
      <button @click="addTask">add</button>
    </div>
    <div v-if="unfinishTasks.length === 0">
      <div class="unfinish">
        <h3>You have no task!</h3>
      </div>
    </div>
    <div v-for="(item, index) in unfinishTasks" :key="item.name">
      <div class="unfinish">
        <div class="name">
          Task: {{ item.name }}
          <button @click="completeTask(index)">complete</button>
        </div>
        <div class="deadline">Deadline: {{ item.deadline }}</div>
      </div>
    </div>
    <div v-if="finishedTasks.length > 0">
      <div class="hilight">
        <h3>Finished</h3>
      </div>
    </div>
    <div v-for="(item,index) in finishedTasks" :key="item.name">
      <div class="finished">
        <div class="name">
          Task: {{ item.name }}
          <button @click="deleteTask(index)">delete</button>
        </div>
        <div class="deadline">Deadline: {{ item.deadline }}</div>
      </div>
    </div>
  </div>
</template>

<style>
.unfinish {
  color: red;
}
.hilight {
  color: darkgreen;
}
.finished {
  color: gray;
}
</style>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      unfinishTasks: [
        { name: "おわってない", deadline: "7/32" },
        { name: "かなりおわってない", deadline: "8/32" }
      ],
      finishedTasks: [{ name: "おわってる", deadline: "6/31" }],
      newTaskName: "",
      newTaskDeadline: "",
      removed: []
    };
  },
  methods: {
    addTask() {
      if (this.newTaskName !== "" && this.newTaskDeadline !== "") {
        this.unfinishTasks.push({
          name: this.newTaskName,
          deadline: this.newTaskDeadline
        });
        this.newTaskName = "";
        this.newTaskDeadline = "";
      }
    },
    completeTask(idx) {
      this.removed = this.unfinishTasks.splice(idx, 1);
      this.finishedTasks.push({
        name: this.removed[0].name,
        deadline: this.removed[0].deadline
      });
    },
    deleteTask(idx) {
      this.finishedTasks.splice(idx, 1);
    }
  }
};
</script>
