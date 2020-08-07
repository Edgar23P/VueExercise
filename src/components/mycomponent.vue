<template>
    <div>
        <TodoList msg="hey"/>
    </div>   
</template>
<script>
import TodoList from './TodoList.vue';

export default {
  name: 'mycomponent',
  components:{
      'TodoList':TodoList
    },
  props: {
    msg: String
  }
}
</script>
