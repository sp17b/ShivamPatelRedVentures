<template>
  <div class="hello">
    <!-- Name and Bot Type Input -->
    <div id="inputLeader">
      <div id="inputs">
        <div id="nameInput">
          <h1 style="color: white; margin-top:40px;">WELCOME TO BOT-O-MAT</h1>
          <h3 style="margin: 40px 0 0;">Please Enter Name </h3>
          <input v-model="name" placeholder="Enter Name">
        </div>

        <!-- Dropdown to select type of bot -->
        <div v-if="name" id="inputSelect">
          <h3 style="margin-top: 10px;"> Select a Bot</h3>
          <select  v-model="selectedBot">
            <option v-for="type in botTypes" :key="type">
              {{type}}
            </option>
          </select>
        </div>
      </div>

      <!-- Leaderboard -->
      <div id="leaderboard">
        <table>
          <thead>
            <tr>
              <th> Bot Name </th>
              <th> Tasks Completed </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="leader in leaderBoard.keys()" :key="leader">
              <td >
                {{leader}}
              </td>
              <td>
                {{leaderBoard.get(leader)}}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>    
    
    <!-- All Active Bots  -->
    <div id="allBots">
      <div id="activeBots" v-for="(name,index) in nameArray" :key="name">
        <instancebot :botName="name" :botType="botTypeArray[index]" :tasks="randomTasks" :taskTime="tasksTime" @finishedAll="removeBot"></instancebot>
      </div>
    </div>
  </div>
</template>

<script>
import instancebot from './instance-bot'
export default {
  name: 'HelloWorld',
  
  components:{
    instancebot
  },

created() {
    this.initializeTime();
  },  
  data(){
    return {
      name: '', //Botname
      botTypes: ["UNIPEDAL","BIPEDAL","QUADRUPEDAL","ARACHNID","RADIAL","AERONAUTICAL"],
      selectedBot: '', //Bot Selected From Dropdown
      selectedBots: new Map(),
      tasksTime: new Map(), //Hold task and time values
      randomTasks: [],//Generate Random Tasks and time for each bot
      nameArray: [], //All current bot names
      botTypeArray: [], //All current bot types
      interval: 0,
      leaderBoard: new Map, //Store the leaderboard info
    }
  },


  watch:{
    selectedBot(newVal){
      if(this.name != '' && newVal != ''){
        this.updateMap();
      }
      this.selectedBot = '';
      this.name = '';
    }
  },

  methods: {
    updateMap: function(){
      if(!this.nameArray.includes(this.name)){
        clearInterval(this.interval);
        this.nameArray.push(this.name);
        this.botTypeArray.push(this.selectedBot);
        this.selectedBots.set(this.name,this.selectedBot);
        this.randomizeTasks();
      }else{
        console.log("Name Already in Use");
      }
    },
    initializeTime: function(){
      if(this.tasksTime.size == 0){
        this.tasksTime.set('do the dishes',1000);
        this.tasksTime.set('sweep the house',3000);
        this.tasksTime.set('do the laundry',10000);
        this.tasksTime.set('take out the recycling',4000);
        this.tasksTime.set('make a sammich',7000);
        this.tasksTime.set('mow the lawn',20000);
        this.tasksTime.set('rake the leaves',18000);
        this.tasksTime.set('give the dog a bath',8000);
        this.tasksTime.set('bake some cookies',1000);
        this.tasksTime.set('wash the car',20000);
      }      
      
    },
    // Randomly select 5 tasks for bot
    randomizeTasks: function(){
      this.randomTasks = [];
      let tempArray = [];
      let keys = Array.from(this.tasksTime.keys());
      //Ensuring no duplicate tasks are assigned
      while(this.randomTasks.length != 5){
        let index = keys[Math.floor(Math.random()*keys.length)];
        if(!tempArray.includes(index)){
          tempArray.push(index);
          this.randomTasks.push(index);
        }
      }
    },
    removeBot: function(name){
      // console.log("IN REMOVE BOT");
      // Find Index of Bot
      if(!this.leaderBoard.has(name.toLowerCase())){
        this.leaderBoard.set(name.toLowerCase(),1);
      }else{
        this.leaderBoard.set(name.toLowerCase(),this.leaderBoard.get(name.toLowerCase())+1);
      }

      let index = this.nameArray.findIndex(n => n === name);
      this.nameArray.splice(index,1);
      this.botTypeArray.splice(index,1);
      console.log(this.nameArray);

    }
  },
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  margin-top: 100px;
}
#inputLeader h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#inputs{
  float: left;
  margin-left: 20%;
}
#inputs h1{
  margin-top: 0px;
}
#inputLeader{
  height: 250px;
  border: #42b983 1px solid;
  background-color:  #8ec3eb;;
}
#allBots{
  margin-top: 20px;
  max-width: 90%;
  display: inline-block;
  position: relative;
  overflow: auto;
}
#leaderboard{
  max-width: 90%;
  float: right;
  overflow-y: auto;
  max-height: 200px;
  margin-right: 20%;
  margin-top: 50px;
}

#activeBots{
  margin: 10px;
  float: left;
}
.hello{
  width: 100%;
  height: 100%;
  display: block;
}
body{
  background-color: black;
}
/* table */
table th, td {
  padding: 5px;
} 
table th,td{
  border: black 1px solid;
}
table thead{
  color: rgb(252, 252, 252);
}
/* Dropdown */
select{
  margin-bottom: 5px;
}

</style>
