#Running Project

-My project is developed using Vue.js framework

Steps:

1.Install Vue is installed 
->1. sudo npm install -g @vue/cli 
->2.sudo npm update -g @vue/cli #To update cli 
->3.npm i @vue/cli-service #Install dependencies
2.Navigate inside bot-o-mat-sp17b Folder
3.Run the command : npm run serve
4.Then go to http://localhost:8080/ in a browser to view the project.

Project Details:
-The landing page has input for a name Ex. Sam -Upon entering the name the user can select the type of bot they want 
-THen 5 random tasks will be displayed which the bot can do -Upon completion of all the tasks, the bot's name and number of tasks will be added to the leaderboard table in upper right. Ex. Sam 1 
-Cannot create a bot with the same name if bot already has tasks assigned however once the bot finishes all the tasks then a new bot with the same nam can be created 
-Clicking on the task time will disable the task button and start the countdown. Once the task is finished the task will be removed from the list. 
-Once all the tasks are finished the bot will be removed.
--------------------------------------------------------------------

BOT-O-MAT
Use any language to complete this challenge. The implementation is up to you: it can be a command-line application or have a graphical interface.

Your application should collect a name and robot type from the types we list below. For each, it should create a Robot of the type the user chooses, e.g. Larry, Bipedal.

Given the list of tasks below, your application should then assign the Robot a set of five tasks, all of which complete after a duration that we show in milliseconds.

Collect a name and robot type from user.
Instantiate a Robot of the type provided by the user with the name provided by the user
for example: Bipedal, Larry
Set up methods on Robot to complete tasks from the provided list
Robot
Robot completes tasks and removes them from the list when they are done (i.e. enough time has passed since starting the task).

Tasks
Tasks have a description and an estimated time to complete.

[
  {
    description: 'do the dishes',
    eta: 1000,
  },{
    description: 'sweep the house',
    eta: 3000,
  },{
    description: 'do the laundry',
    eta: 10000,
  },{
    description: 'take out the recycling',
    eta: 4000,
  },{
    description: 'make a sammich',
    eta: 7000,
  },{
    description: 'mow the lawn',
    eta: 20000,
  },{
    description: 'rake the leaves',
    eta: 18000,
  },{
    description: 'give the dog a bath',
    eta: 14500,
  },{
    description: 'bake some cookies',
    eta: 8000,
  },{
    description: 'wash the car',
    eta: 20000,
  },
]
Types
{ 
  UNIPEDAL: 'Unipedal',
  BIPEDAL: 'Bipedal',
  QUADRUPEDAL: 'Quadrupedal',
  ARACHNID: 'Arachnid',
  RADIAL: 'Radial',
  AERONAUTICAL: 'Aeronautical'
}
Features to add once the core functionality is complete
Be creative and have fun! Use this list or create your own features.

Allow users to create multiple robots at one time
Create a leaderboard for tasks completed by each Robot
Create tasks specific for each robot type, this could work in conjunction with the leaderboard. For e.g. robots that are assigned tasks that their type can’t perform won’t get “credit” for finishing the task.
Add persistance for tasks, bots and leaderboard stats
Privacy Guidelines
Due to the creative nature of this project, please do not post the prompt or your solution publicly. Feel free to privately fork it to your personal GitHub or download it for future reference, as this workspace is cleared every few months.

Authors
Scott Hoffman https://github.com/scottshane
Olivia Osby https://github.com/oosby
