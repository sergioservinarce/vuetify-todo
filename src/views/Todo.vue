<template>
  <div class="home">

    <list-tasks 
      v-if="$store.state.tasks.length"
    />

    <no-tasks
      v-else
    />

  <btn-done-sorting  v-if="$store.state.sorting"/>


  </div>
</template>

<script>

// @ is an alias to /src
export default {
  name: 'Home',
  
  components: {
    'list-tasks' : require('@/components/Todo/ListTasks.vue').default,
    'no-tasks' : require('@/components/Todo/NoTasks.vue').default,
    'btn-done-sorting' : require('@/components/Todo/ButtonDoneSorting.vue').default
  }
}
</script>
