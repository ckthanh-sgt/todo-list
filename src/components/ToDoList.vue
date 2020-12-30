<template>
  <v-container id="frmToDo">
    <h3 class="frmToDoTitle">Todo Application</h3>
    <v-form
      ref="form"
      lazy-validation>
      <v-container>
        <v-row>
          <v-col cols="12">
            <v-text-field
              v-model="todoName"
              :counter="255"
              label="Task name"
              prend-icon=""
              required
            >
              <i
                class="fa fa-arrow-right submit-icon"
                aria-hidden="true"
              ></i>
            </v-text-field>
          </v-col>
          <v-col cols="12">
            <v-textarea
              v-model="todoDescription"
              label="Description"
              value=""
              cols="50"
            ></v-textarea>
          </v-col>
        </v-row>
        <v-row class="frmFunction">
          <v-col cols="12">
            <v-btn
              class="v-btn--rounded mr-2"
              @click="addTodo"
            >
              Add
            </v-btn>
            <v-btn
              class="v-btn--rounded"
              @click="clearForm"
            >
              Clear
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
    <table class="table" id="listTodoes">
      <thead>
      <tr>
        <th scope="col">Order</th>
        <th scope="col">Task Name</th>
        <th scope="col">Date</th>
        <th scope="col">Actions</th>
      </tr>
      </thead>
      <tbody>
      <tr
        v-for="todo in todoes"
        v-if="todo.status"
        v-bind:key="todo.id"
      >
        <th scope="row">{{todo.id}}</th>
        <td>{{todo.todoName}}</td>
        <td>{{todo.created_at}}</td>
        <td>
          <button
            @click="editTodo"
            type="button"
            aria-label="Edit"
            title="Edit"
            class="btn btn-primary text-white"
          >
            Edit
          </button>
          <button
            @click="removeTodo"
            type="button"
            aria-label="Delete"
            title="Delete"
            class="btn btn-danger text-white"
          >
            Delete
          </button>
        </td>
      </tr>
      </tbody>
    </table>
  </v-container>
</template>

<script>

export default {
  name: 'ToDoList',
  data: () => ({
    search: '',
    todoName: '',
    todoDescription: '',
    todoes: [
      {
        'id': 1,
        'created_at': '2020-12-30',
        'updated_at': '',
        'deleted_at': '',
        'todoName': 'Meeting with customer at 18:00pm',
        'todoDescription': 'Have an appointment with VIP Customer at 18:00pm',
        'status': 1
      },
      {
        'id': 2,
        'created_at': '2020-12-30',
        'updated_at': '',
        'deleted_at': '',
        'todoName': 'Meeting with customer at 20:00pm',
        'todoDescription': 'Have an appointment with VIP Customer at 20:00pm',
        'status': 1
      },
      {
        'id': 3,
        'created_at': '2020-12-30',
        'updated_at': '',
        'deleted_at': '',
        'todoName': 'Meeting with customer at 22:00pm',
        'todoDescription': 'Have an appointment with VIP Customer at 22:00pm',
        'status': 1
      }
    ]
  }),
  methods: {
    addTodo: function () {
      alert('Add todo')
    },
    editTodo: function () {
      alert('Edit todo')
    },
    removeTodo: function () {
      alert('Are you sure to delete?')
    },
    clearForm: function () {
      alert('Clear form data')
    }
  }
}
</script>

<style scoped>
#frmToDo {
  margin: 0 auto;
  background: white;
  position: absolute;
  min-height: 800px;
  max-width: 800px;
  top: calc(50% - 450px);
  left: calc(50% - 400px);
  padding: 30px 20px;
}

h3.frmToDoTitle {
  padding: 0px 11px;
}

.frmFunction {
  text-align: right;
}

.frmFunction button:first-child {
  margin-right: 13px;
}

table#listTodoes {
  margin-top: 32px;
}
</style>
