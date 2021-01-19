<template>
  <div>
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <form @submit="addTodo">
          <input
            type="text"
            id="title"
            name="title"
            v-model="title"
            placeholder="Add Todo.."
            class="form-control"
          />
          <input
            type="submit"
            name="submit"
            value="Submit"
            class="btn btn-dark"
          />
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false,
      };
      console.log(newTodo);
      //send upto parent
      this.$emit("add-todo", newTodo);
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 20px;
  border-radius: 1px 1px 4px 0px;
  border-bottom: 0!important;
}
input[type="submit"] {
  /* flex: 2; */
  border-radius: 1px 1px 4px 0px!important;
}
.btn:hover {
  background: #666;
}

</style>