<template>
  <div class="list-task m-4">
    <h1>Todo List</h1>
    <p v-show="tasks.length == 0">Belum ada task</p>
    <div
      v-for="(item, index) of tasks"
      class="item-task d-flex align-items-start border-bottom pt-3 pb-4"
      :key="item.id"
    >
      <input
        type="checkbox"
        name="status"
        id="task"
        class="me-2 mt-2 form-check-input checkbox"
        :checked="item.isDone"
        @change="updateTaskStatus(index)"
      />
      <div class="d-flex flex-column">
        <div class="title-task mb-1">
          <s v-if="item.isDone">{{ item.title }}</s>
          <span v-else>{{ item.title }}</span>
        </div>
        <div class="description-task small text-muted">
          {{ item.description }}
        </div>
        <a href="#" class="link-primary" @click="deleteTask($event, index)"
          >Delete</a
        >
      </div>
    </div>
    <div class="action py-2">
      <a
        href="#"
        class="add-button"
        v-if="!isCreating"
        @click="isCreating = !isCreating"
        >Add Task</a
      >
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-0">
            <input
              class="form-control border-0 mb-2"
              placeholder="Title"
              type="text"
              v-model="titleValue"
            />
            <textarea
              class="form-control border-0 small"
              placeholder="Description"
              rows="3"
              v-model="descriptionValue"
            ></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button class="btn btn-primary me-2" @click="addTask">Save</button>
          <button
            class="btn btn-outline-secondary"
            @click="isCreating = !isCreating"
          >
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.checkbox:checked { background-color: rgb(126, 126, 126); }
</style>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

export default {
  data() {
    return {
      tasks: [],
      isCreating: false,
      titleValue: "",
      descriptionValue: "",
    };
  },
  methods: {
    addTask() {
      this.tasks.push({
        id: this.tasks.length + 1,
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      });
      this.isCreating = !this.isCreating;
      this.titleValue = "";
      this.descriptionValue = "";
    },
    deleteTask(event, index) {
      const targetElement = event.target;
      targetElement.parentElement.remove();
      this.tasks.splice(index, 1);
    },
    updateTaskStatus(index) {
      this.tasks[index].isDone = !this.tasks[index].isDone;
    },
  },
};
</script>
