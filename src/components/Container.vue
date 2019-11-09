<template>
        <div class="content">
            <div class="card-content">
                 <input v-if ="add_flag" type="text" class="add" v-model = "add_data" @keyup.enter = "add_task">
            <div class="card"
            v-for="(todo,index) in todos" :key="index"
            >
                <div class="card-content-inner">
                    <p>{{ todo.task }}</p>
                    <div class="btn-box pull-right">
                    <button class = 'button button-success'
                    :class = "{'button-fill':todo.done}"
                     @click="task_flag(index)"
                     >
                    <i class = "icon icon-check"></i>
                    </button>
                    <button class = "button button-danger"
                    @click = "rem_task(index)"
                    >
                        <i class="icon icon-remove"></i>
                    </button>
                    </div>
                </div>
                </div>
            </div>
        </div>
</template>

<script>
export default {
    props:['todos','add_flag'],
  data(){
      return{
           add_data:''
      }
  },
  methods: {
    task_flag(index) {
        this.todos[index].done = !this.todos[index].done
    },
    rem_task(index){
        this.$emit('del_task',index)
    },
    add_task(){
        console.log(1)
        this.$emit('add_task',this.add_data)
    }


  }

}
</script>

<style scoped lang="stylus">

</style>
