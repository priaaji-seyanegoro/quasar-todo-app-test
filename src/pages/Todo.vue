<template>
  <q-page class="bg-grey-3 column">
    <q-list class="bg-white" separator bordered v-for="task in tasks" :key="task.title">
      <q-item v-ripple @click="task.done = !task.done" clickable :class="{done : task.done}">
        <q-item-section avatar>
          <q-checkbox class="no-pointer-events"  v-model="task.done" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  name: 'Todo',
  data(){
    return{
      tasks : [
        {
          title: 'Get banana',
          done : false
        },
        {
          title: 'Eat banana',
          done : false
        },
        {
          title: 'Poo banana',
          done : false
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
  .done{
    .q-item__label{
      text-decoration: line-through;
      color: #bbb;
    }
  }
</style>
