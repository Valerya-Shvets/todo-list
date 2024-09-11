<template>
  <div class="todo-list">
    <div class="new-task__field">
      <input
        class="new-task__input"
        type="text"
        v-model="newTask"
        placeholder="Input task"
      />
      <button class="new-task__button" v-on:click="addTask">Add</button>
    </div>
    <div class="scroll-field">
      <ul class="task-list">
        <li class="task-list__item" v-for="(task, key) in tasks">
          <span class="task-list__paragraph">{{ task }}</span>
          <div>
            <span
              class="task-list__span-done"
              v-on:click="finishTask(key)"
              title="done"
              >✔</span
            >
            <span
              class="task-list__span-remove"
              v-on:click="deleteTask(key)"
              title="remove"
              >✘</span
            >
          </div>
        </li>
      </ul>
    </div>

    <div class="finished-field" v-show="finished.length > 0">
      <hr class="line" />
      <ul class="finished-list">
        <li class="finished-list__item" v-for="finish in finished">
          <p class="finished-list__paragraph">{{ finish }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
      finished: [],
    };
  },
  methods: {
    addTask() {
      this.tasks.push(this.newTask);
      this.newTask = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    finishTask(index) {
      this.finished.push(this.tasks[index]);
      this.deleteTask(index);
      console.log("Tasks", this.tasks);
      console.log("Finished", this.finished);
    },
  },
  computed: {},
};
</script>

<style scoped>
.todo-list {
  padding-left: 30px;
  padding-right: 30px;
  padding-top: 40px;
  padding-bottom: 40px;
  border-radius: 15px;
  background-color: #ffffff;
  width: 30%;
  height: 500px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 100px;
  box-shadow: 10px 10px 10px rgba(128, 128, 128, 0.5);
}
.new-task__field {
  display: flex;
  align-items: center;
  justify-content: space-between;
  column-gap: 25px;
}
.new-task__input {
  padding: 10px;
  font-size: 20px;
  font-family: "SUSE", sans-serif;
  font-weight: 400;
  width: 100%;
  border-radius: 5px;
  border: 2px solid grey;
  transition: border-color 300ms ease;
}
.new-task__input:focus {
  border-color: #219ebc;
  outline: none;
}
.new-task__button {
  cursor: pointer;
  font-size: 20px;
  font-weight: 500;
  font-family: "SUSE", sans-serif;
  padding: 11px 20px;
  border-radius: 5px;
  border: 2px solid #219ebc;
  background-color: #219ebc;
  color: #ffffff;
  text-align: center;
  transition: all 300ms ease;
}
.new-task__button:hover {
  background-color: transparent;
  color: #219ebc;
}
.scroll-field {
  display: block;
  margin-top: 40px;
  margin-bottom: 30px;
  max-height: calc(100% - 70px);
  overflow-y: auto;
  scrollbar-gutter: stable;
  scrollbar-color: #219ebc transparent;
  scrollbar-width: thin;
}
.task-list {
  display: flex;
  flex-direction: column;
  row-gap: 20px;
  list-style: none;
  padding-left: 0;
}
.task-list__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #219dbc75;

  border: 1px solid rgba(104, 99, 99, 0.612);
  border-radius: 5px;
  padding: 10px;
}
.task-list__paragraph {
  font-size: 20px;
  font-weight: 300;
  font-family: "SUSE", sans-serif;
}
.task-list__span-remove {
  cursor: pointer;
  padding: 7px 15px;
  color: #ce1919;
  font-family: "SUSE", sans-serif;
  font-size: 20px;
  font-weight: 700;
  border-radius: 5px;
  transition: color 300ms ease;
}
.task-list__span-done {
  cursor: pointer;
  padding: 7px 15px;
  color: #048f3a;
  font-family: "SUSE", sans-serif;
  font-size: 20px;
  font-weight: 700;
  border-radius: 5px;
  transition: color 300ms ease;
}
.task-list__span-remove:hover,
.task-list__span-done:hover {
  color: #ffffff;
}
.finished-field {
  position: absolute;
  top: 100px;
  right: 50px;
  width: 25%;
  max-height: 200px;
  padding-left: 30px;
  padding-right: 30px;
  padding-top: 40px;
  padding-bottom: 5px;
  border-radius: 15px;
  background-color: #ffffff;
  box-shadow: 10px 10px 10px rgba(128, 128, 128, 0.5);
  overflow-y: auto;
  scrollbar-color: #219ebc rgba(202, 202, 202, 0.132);
  scrollbar-width: thin;
}
.line {
  border: 1px solid rgba(104, 99, 99, 0.119);
}
.finished-list {
  list-style: none;
  padding-left: 0;
}
.finished-list__paragraph {
  font-family: "SUSE", sans-serif;
  font-size: 20px;
  font-weight: 500;
  color: rgba(104, 99, 99, 0.4);
  text-decoration: line-through;
  margin-top: 0;
  margin-bottom: 10px;
}
</style>
