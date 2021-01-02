<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        class="col"
        filled
        placeholder="Add New Task"
        square
        bg-color="white"
        dense
        @keyup.enter="addNewTask"
      >
        <template v-slot:append>
          <q-btn round dense flat icon="add" @click="addNewTask" />
        </template>
      </q-input>
    </div>
    <q-list
      class="bg-white"
      separator
      bordered
      v-for="(task, index) in tasks"
      :key="task.title"
    >
      <q-item
        v-ripple
        @click="task.done = !task.done"
        clickable
        :class="{ 'done bg-blue-1 ': task.done }"
      >
        <q-item-section avatar>
          <q-checkbox
            class="no-pointer-events"
            v-model="task.done"
            color="primary"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side @click="deleteTask(index)">
          <q-btn flat round dense color="primary" icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>

    <div class="div no-task absolute-center" v-if="!tasks.length">
      <q-icon name="check" size="100px" color="primary" />
      <div class="div text-h5 text-primary text-center">
        No Tasks
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      newTask: "",
      tasks: [
        // {
        //   title: "Get banana",
        //   done: false
        // },
        // {
        //   title: "Eat banana",
        //   done: false
        // },
        // {
        //   title: "Poo banana",
        //   done: false
        // }
      ]
    };
  },
  methods: {
    deleteTask(index) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Are You Sure?",
          cancel: true,
          persistent: true
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          this.$q.notify({
            message: "Delete successfully",
            position: "top-right",
            color: "red"
          });
        });
    },
    addNewTask() {
      this.tasks.push({
        title: this.newTask,
        done: false
      });
      this.newTask = "";
    }
  }
};
</script>

<style lang="scss" scoped>
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #bbb;
  }
}
.no-task {
  opacity: 0.5;
}
</style>
