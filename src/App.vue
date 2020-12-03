<template>
  <div id="app">
    <Kanban :data="data" :create_task_submit="create_task_submit" />
  </div>
</template>

<script>
import Kanban from './components/Kanban.vue'

export default {
  name: 'App',
  components: {
    Kanban
  },
  data(){
    return{
      data:[
        {
          name:"todo",
          color:"#EB5757",
          tasks:[
            {
              task_name:"test"
            }

          ]
        },
        {
          name:"doing",
          color:"#219653",
          tasks:[
            {
              task_name:"test"
            }
          ]
        },
        {
          name:"done",
          color:"#2F80ED",
          tasks:[
             {
              task_name:"test"
            }
          ]
        }
      ]
    }
  },
  methods:{
    create_task_submit(colume_index,item){
      this.data[colume_index].tasks.push(item)
    }
  }
}
</script>

<style>
#app {
  height: 100vh;

}
</style>
