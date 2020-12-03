<template>
  <div id="app">
    <Kanban :data="data" :create_task_submit="create_task_submit" :move_item_task="move_item_task"/>
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
    },
    move_item_task(calume_a,index_task_a,colume_b,index_task_b){
      var item = this.data[calume_a].tasks[index_task_a]
      this.data[calume_a].tasks.splice(index_task_a,1)
      this.data[colume_b].tasks.splice(index_task_b,0,item)
    },
  }
}
</script>

<style>
#app {
  height: 100vh;

}
</style>
