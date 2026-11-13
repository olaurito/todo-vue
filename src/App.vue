<template>
   <!-- Content -->
    <div class="px-3 py-10 md:px-10">
        <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
         <!-- <pre>{{ $store.state.todos }}</pre> -->
          <TodoSpinner v-if="loading" />

            <div v-else>
                <TodoFormAdd />


                <TodoItems v-if="$store.state.todos.length" />

                <TodoEmpty v-else />
          </div>
        </div>
    </div>
    <!--/ Content -->
</template>

<script>
import TodoFormAdd from './components/TodoFormAdd.vue';
import TodoSpinner from './components/TodoSpinner.vue';
import TodoItems from './components/TodoItems.vue';
import TodoEmpty from './components/TodoEmpty.vue';

export default {
  name: 'App',
  components: { TodoFormAdd, TodoSpinner, TodoItems, TodoEmpty  },

  data() {
    return {
      loading: false
    }
  },
  created() {
    this.loading = true;
    this.$store.dispatch('getTodos')
      .then(() => {
        this.loading = false;
      })
      .catch(error => {
        console.error(error);
        this.loading = false;
      })
      .finally(() => {
        this.loading = false;
      });
    
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
