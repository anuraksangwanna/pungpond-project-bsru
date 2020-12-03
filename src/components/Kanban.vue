<template>
   <div class="kanban">
     <div class="colume" :style="{backgroundColor:colume.color}" v-for="(colume , index) in data" :key="index">
        <div class="colume-header">
            {{colume.name}}
        </div>
        <div class="colume-body">
            <div  v-for="(task,task_index) in colume.tasks" :key="task_index">
                <div class="task"
                    :draggable="true"
                     @dragstart="start_move(task_index,index)"
                >
                {{task.task_name}}
            </div>

            </div>
            <div class="drop_zone" 
            @dragenter.prevent="drop_zone_enter" 
            @dragleave.prevent="drop_zone_leave" 
            @dragover.prevent
            >

            </div>
            <div class="create-task" @click="create_task(index)">Create Task</div>
        </div>
     </div>
    <b-modal ref="create-task-model" title="Create Task">
        <input class="input-task-name" v-model="task_name" @keyup.13="submit_create_task" />
    </b-modal>
   </div>
</template>
<script>
export default {
    props:{
        data:Array,
        create_task_submit:Function
    },
    methods:{
        create_task(index_colume){
            this.current_colume_index = index_colume
            this.$refs["create-task-model"].show()
        },
        submit_create_task(){
            this.create_task_submit(this.current_colume_index,{task_name: this.task_name})
            
        },
        start_move(task_index,colume_index){
                this.current_colume_index= colume_index
                this.current_task_index= task_index
        },
        drop_zone_enter(event){
                event.target.style.height = "100px";
                event.target.style.borderStyle = "dotted";
                event.target.style.transition = "height 0.5s"
        },
        drop_zone_leave(event){
                event.target.style.height = "10px";
                event.target.style.borderStyle = "none";
                event.target.style.transition = "height 0.5s";
        }
    },
    data(){
        return{
            task_name:"",
            current_colume_index:"",
            current_task_index:""
        }
    }
}
</script>

<style>
    .kanban{
        width: 100%;
        height: 100%;
        background-color: sandybrown;
    }
    .colume{
         width: 300px;
        height: 600px;
        margin: 15px;
        border-radius: 10px;
        display: inline-block;
        -webkit-box-shadow: 5px 3px 11px 3px rgba(26,18,26,1);
        -moz-box-shadow: 5px 3px 11px 3px rgba(26,18,26,1);
        box-shadow: 5px 3px 11px 3px rgba(26,18,26,1);
        padding: 10px   ;
    }
    .colume-header{
        display: flex;
        align-items: center;
        justify-content: center;
        height: 50px;
        font-size: 32px;
        font-weight: bold;
    }
    .colume-body{
        height: calc(100% - 50px);
        border-radius: 10px;
        padding: 5px;
        background-color: rgba(255, 245, 238, 0.24);
        
    }
    .create-task{
        width: 100%;
        height: auto;
        padding: 10px;
        border-radius: 5px;
        cursor: pointer;
        ;
    }
    .create-task:hover{
        background-color: rgba(241, 245, 242, 0.397);
    }
    .input-task-name{
        width: 100%;
    }
    .task{
        width: auto;
        position: relative;
        height: 100px;
        border-radius: 10px;
        margin: 10px;
        background-color: rgb(212, 231, 44);
    }
    .drop_zone{
            height: 10px;
    }
</style>