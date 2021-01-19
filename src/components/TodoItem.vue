<template>
  <div>
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <div class="card">
          <div class="card-body">
            <div
              class="todo-item"
              v-bind:class="{ 'is-complete': todo.completed }"
            >
              <ul class="list-group">
                <li class="list-group-item">
                  <input type="checkbox" v-on:change="markComplete" class="" />
                  {{ todo.title }}
                  <button
                    @click="$emit('del-todo', todo.id)"
                    class="btn btn-sm btn-danger float-right delete"
                  >
                    X
                  </button>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      //  console.log(this.todo.completed);
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style  scoped>

.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
}
.list-group-item {
  text-align: initial !important;
}
.card {
  background: #f8f8f8 !important;
}
</style>