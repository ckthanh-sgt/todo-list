<template>
  <v-container id="frmToDo">
    <h3 class="frmToDoTitle">Todo Application</h3>
    <v-form
      id="frm_ToDo"
      method="post"
      action="."
    >
      <div id="errors" v-if="errors.length">
        <ul>
          <li
            class="btn btn-danger text-white"
            v-for="(error, key) in errors"
            :key="key"
          >
            {{ error }}
          </li>
        </ul>
      </div>

      <v-container>
        <v-row>
          <v-col cols="12">
            <v-text-field
              v-model="todoName"
              :counter="255"
              label="Task name"
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
              type="button"
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
        <th>
          <input type="checkbox" @click="checkAll(true)">
        </th>
        <th scope="col">Order</th>
        <th scope="col">Task Name</th>
        <th scope="col">Date</th>
        <th scope="col">Status</th>
        <th scope="col">Actions</th>
      </tr>
      </thead>
      <tbody>
      <tr
        v-for="(todo, key) in todoes"
        :key="key"
        :class="{ 'done-task' : todo.completed }"
      >
        <th>
          <input type="checkbox" value="" class="">
          <v-input
            type="checkbox"
            :checked="todo.checked"
          ></v-input>
        </th>
        <th>{{ todo.id }}</th>
        <td>{{ todo.todoName }}</td>
        <td>{{ todo.created_at }}</td>
        <td>
          {{ todo.status === 1 ? 'Done' : 'Doing' }}
        </td>
        <td>
          <div v-if="!todo.completed">
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
              @click="removeTodo(key)"
              type="button"
              aria-label="Delete"
              title="Delete"
              class="btn btn-danger text-white"
            >
              Delete
            </button>
          </div>
          <div v-else>
            <button
              @click="viewTodo(todo.id)"
              type="button"
              title="Undo"
              class="btn btn-warning text-white"
            >
              View
            </button>
          </div>
        </td>
      </tr>
      </tbody>
    </table>
  </v-container>
</template>

<script>
import moment from 'moment'

export default {
  name: 'ToDoList',
  beforeCreate () {
    console.log('Before Create Function: Nothing starts before me!')
  },
  data: () => ({
    search: '',
    errors: [],
    deleted_at: '',
    todoName: '',
    todoDescription: '',
    status: '',
    completed: '',
    checked: false,
    todoes: [
      {
        'id': 1,
        'created_at': '2020-12-30',
        'updated_at': '',
        'deleted_at': '',
        'todoName': 'Meeting with customer at 18:00pm',
        'todoDescription': 'Have an appointment with VIP Customer at 18:00pm',
        'status': 0,
        'completed': 0,
        'checked': false
      },
      {
        'id': 2,
        'created_at': '2020-12-30',
        'updated_at': '',
        'deleted_at': '',
        'todoName': 'Meeting with customer at 20:00pm',
        'todoDescription': 'Have an appointment with VIP Customer at 20:00pm',
        'status': 1,
        'completed': 1,
        'checked': false
      },
      {
        'id': 3,
        'created_at': '2020-12-30',
        'updated_at': '',
        'deleted_at': '',
        'todoName': 'Meeting with customer at 22:00pm',
        'todoDescription': 'Have an appointment with VIP Customer at 22:00pm',
        'status': 1,
        'completed': 1,
        'checked': false
      }
    ]
  }),
  methods: {
    addTodo: function () {
      // Check validation
      if (this.todoName.trim().length === 0) {
        this.errors.push('Please enter task name')
        return
      }

      if (this.todoDescription.trim().length === 0) {
        this.errors.push('Please enter some descriptions')
        return
      }

      // Add data
      this.todoes.push({
        'id': this.todoes.length + 1,
        'created_at': moment().format('YYYY-MM-DD'),
        'updated_at': '',
        'deleted_at': '',
        'todoName': this.todoName,
        'todoDescription': this.todoDescription,
        'status': 1,
        'completed': 0,
        'checked': false
      })

      // Clear all data after success
      while (this.errors.length > 0) {
        this.errors.pop()
      }
      // Clear input data after success
      this.$data.todoName = ''
      this.$data.todoDescription = ''
    },
    editTodo: function () {
      alert('Edit todo')
    },
    removeTodo: function (key) {
      if (confirm('Are you sure to delete?')) {
        // Method One:
        // this.$delete(this.todoes, key)

        // Method Two:
        this.todoes.splice(key, 1)
      }
    },
    clearForm: function (e) {
      e.preventDefault()
      this.$data.todoName = ' '
      this.$data.todoDescription = ' '
      this.errors = []
    },
    checkAll: function (flag) {
      alert('Check all' + flag)
      this.todoes.forEach(todo => {
        todo.checked = flag
      })
    },
    viewTodo: function (key) {
      alert('View task: ' + key)
    }
  },
  computed: {
    // Get total of tasks
    totalTasks: function () {
      return this.totalTasks + ' ' + this.todoDescription
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
  max-width: 1100px;
  top: calc(50% - 450px);
  left: calc(50% - 550px);
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

.done-task {
  color: darkorange;
  text-decoration: line-through;
}

#errors ul {
  padding-left: 11px;
  list-style: none;
  margin-top: 20px;
}

#errors ul li {
  margin-right: 12px;
}
</style>
