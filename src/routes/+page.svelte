<script lang="ts">
  interface Tasks {
    id: number;
    title: string;
    isCompleted: boolean;
  }
  let TaskName = "";
  let num: number = 0;
  let taskList: Tasks[] = [];
  let numberOfTask:number;
  let taskCounter:number=0
  let taskCompletion:number;
  

  const handleClick = (e: Event) => {
    e.preventDefault();
    if(TaskName){
    let newTask: Tasks = { id: num, title: TaskName, isCompleted: false };
    taskList = [...taskList, newTask];
    numberOfTask=taskList.length;
    TaskName = "";
    num++;
    taskCompletion=(Math.ceil(taskCounter/numberOfTask*100))
  }
  };
  const taskState = (index: number) => {
    console.log((taskList[index].isCompleted = true));
    taskCounter++
    taskCompletion=(Math.ceil(taskCounter/numberOfTask*100))
  };
  const reset = ()=>{
    taskList=[];
    taskCompletion=0;
    numberOfTask=0
    taskCounter=0
  }
  
</script>

<div class="h-screen bg-gray-900 flex items-center flex-col ">
  <div class="mt-44">
    <form action="" class="flex w-screen justify-center justify-evenly md:justify-center">
      <input type="text" 
             placeholder="Enter Task" 
             bind:value={TaskName}
             class="bg-gray-700 border border-white text-white text-center text-md rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-1/3 md:mr-2" />
      <button type="submit" 
              on:click={handleClick} 
              class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-3 py-2.5 text-center md:ml-2">Add Task</button>
              <button type="submit" 
              on:click={reset} 
              class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-3 py-2.5 text-center md:ml-2">Reset Tasks</button>
    </form>
  </div>

  <div>
    <h1 class="text-center mt-8 mb-4 text-2xl text-white ">{taskCompletion?`${taskCompletion}% Task Completed`:'Task List '} </h1>
    <div>
      <table class="w-full text-sm text-left rtl:text-right text-gray-500 ">
        <thead class="text-xs text-white uppercase bg-gray-700 ">
          <tr class="text-white">
            <th scope="col" class="px-6 py-3">Sr</th>
            <th scope="col" class="px-6 py-3">Task Name</th>
            <th scope="col" class="px-6 py-3">Done ?</th>
          </tr>
        </thead>
        <tbody >
          {#each taskList as task, index (task.id)}
            <tr class="border-b bg-gray-800 border-gray-700 text-white">
              <td class="px-6 py-4">{index + 1}</td>
              <td class={`px-6 py-4  ${task.isCompleted?"line-through text-gray-400":"none"} `}>{task.title}</td>
              <td
                  class="px-4 py-4 flex justify-evenly"
                >
                <button 
                class="text-white bg-green-700 hover:bg-green-800 focus:outline-none focus:ring-4 focus:ring-green-300 font-medium rounded-full text-sm px-5 py-1 text-center "
                on:click={() =>taskState(index)}
                  > Done </button></td
              >
            </tr>
          {/each}
        </tbody>
      </table>
    </div>
  </div>
</div>
