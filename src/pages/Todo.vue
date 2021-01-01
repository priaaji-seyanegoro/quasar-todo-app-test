<template>
  <q-page class="bg-grey-3 column">
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
  </q-page>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      tasks: [
        {
          title: "Get banana",
          done: false
        },
        {
          title: "Eat banana",
          done: false
        },
        {
          title: "Poo banana",
          done: false
        }
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
          this.$q.notify("Task Deleted Success");
        });
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
</style>
