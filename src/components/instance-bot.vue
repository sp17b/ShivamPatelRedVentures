<template>
    <div>
        <!-- Display name and botType -->
        <div id="heading">
            <h1 id="name">{{botName}} : {{botType}}</h1>
        </div>
        <!-- Display Tasks -->
        <div >
            <div v-for="(task,index) in copyTasks" :key="task">
                <div id="timeData" v-if="task != ''">
                    <h3>{{task}}</h3>                    
                    <button :disabled="timerBool[index]" v-on:click="startCountdown(index)"> {{this.milliSeconds[index]}}</button>
                </div>
            </div>
        </div>
    </div>
</template>


<script>

export default{
    name: 'instancebot',

    props:{
        tasks: Array,
        botName: String,
        botType: String,
        taskTime: Map
    },
    created() {
        // Populates arrays with default values
        for(let i =0; i < this.tasks.length; i++){
            this.timerBool.push(false);
            this.milliSeconds.push(this.taskTime.get(this.tasks[i]));
        }
    },

    data(){
        return{
            milliSeconds: [], //Stores time in milleseconds
            timerBool: [], //Stores values if task started
            copyTasks: this.tasks, //Copy of tasks array
            counter: this.tasks.length //Counter decrements when task is finished
        }
    },
    watch:{
        counter(val){
            // If all tasks completed then remove bot
            if(val == 0){
                this.$emit('finishedAll',this.botName);
            }
        }
    },
    methods: {
        // Starts Task Countdown
        startCountdown: function(index){
            this.timerBool[index] = true;
            setTimeout(this.initiateCountdown.bind(null,index),this.milliSeconds[index]);           
        },
        initiateCountdown: function(index){
            this.copyTasks[index] = '';
            this.counter--;
        },

   
    },
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Fira+Sans:wght@200&family=Oswald:wght@200&display=swap');
#heading{
    padding: 15px;
    background-color:#2a6592;
    color: white;
}
#name{
    margin: 0;
}
#timeData{
    background-color: #8ec3eb;
    padding-top: 10px;
    padding-bottom: 10px;
    color: white;
    /* font-weight: bold; */
    font-family: 'Fira Sans', sans-serif;
}
h3{
    margin: 0px;
}
button{
     padding: 6px 12px; 
    margin-top: 12px;
    color: black;
}
</style>