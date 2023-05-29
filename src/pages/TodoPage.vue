<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        class="col"
        square
        @keyup.enter="addTodo"
        v-model="newTodo"
        bg-color="white"
        placeholder="Add Todo"
        dense
      >
        <template v-slot:append>
          <q-btn @click="addTodo" round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white" separator bordered>
      <q-item
        v-for="(task, index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        :class="{ 'done bg-blue-1': task.done }"
        clickable
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            color="primary"
            class="no-pointer-events"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-item-label>
            <q-btn
              @click.stop="deleteTask(index)"
              flat
              dense
              round
              color="red"
              icon="delete"
            />
          </q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary" />
      <div class="text-h5 text-primary text-center">No Tasks</div>
    </div>
  </q-page>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import { Dialog, Notify } from 'quasar';

const newTodo = ref('');
const tasks = ref([
  { title: 'Eat Bananas', done: true },
  { title: 'Learn Qausar', done: false },
  { title: 'Code the World', done: false },
]);

const deleteTask = (index: number) => {
  Dialog.create({
    title: 'Confirm',
    message: 'Would you like to Delete complete Task',
    cancel: true,
    persistent: true,
  }).onOk(() => {
    tasks.value.splice(index, 1);
    Notify.create({ message: 'Todo Deleted successfully', color: 'grey' });
  });
};

const addTodo = () => {
  tasks.value.unshift({
    title: newTodo.value,
    done: false,
  });
  newTodo.value = '';
};
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #bbb;
  }
}

.no-tasks {
  opacity: 0.5;
}
</style>
