<script lang="ts">
  import InnerCard from "./InnerCard.svelte"
  let tasks = $state([
    {title: "Hello", description: "This is a sample task"},
    {title: "Hi again", description: "This is a another sample task"},
  ])
  let titlee = $state("Hi");
  let descriptione = $state("Hi");
  function addTask(){
    if(titlee != "" && titlee != ""){
      tasks = [...tasks, {title: titlee, description: descriptione}];
      titlee = "";
      descriptione = "";
    }
  }
  function deleteTask(task:{title: string, description: string}){
    tasks = [...tasks.slice(0, tasks.indexOf(task)), ...tasks.slice(tasks.indexOf(task) + 1)];
  }
  $inspect(tasks)
</script>

<div class="h-full p-2">
  <div class="border-b border-gray-900/10 pb-12 p-8">
    <h2 class="text-base/7 font-semibold text-gray-900">Add a task</h2>
    <p class="mt-1 text-sm/6 text-gray-600">Enter the task details.</p>
  
    <div class="mt-10 grid grid-cols-1 gap-x-6 gap-y-8 sm:grid-cols-6">
      <div class="sm:col-span-3">
        <label for="title" class="block text-sm/6 font-medium text-gray-900">Title</label>
        <div class="mt-2">
          <input type="text" name="title" id="title" autocomplete="given-name" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm/6" bind:value={titlee}>
        </div>
      </div>
  
      <div class="sm:col-span-3">
        <label for="description" class="block text-sm/6 font-medium text-gray-900">Description</label>
        <div class="mt-2">
          <input type="text" name="description" id="description" autocomplete="family-name" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm/6" bind:value={descriptione}>
        </div>
      </div>
    </div>
  </div>
  <div class="mt-6 flex items-center justify-end gap-x-6">
    <button type="submit" onclick={addTask} class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Add</button>
  </div>

  <ul class="dark:bg-slate-800">
    {#each tasks as task}
      <div class="dark p-6">
        <div class="max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-slate-800 dark:border-gray-700">
          <InnerCard
            {...task}
          />
          <button onclick={() => {deleteTask(task)}} class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-red-700 rounded-lg hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800">
            Task is done
            <svg class="rtl:rotate-180 w-3.5 h-3.5 ms-2" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 10">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5h12m0 0L9 1m4 4L9 9"/>
            </svg>
          </button>
        </div>
      </div>
    {/each}
  </ul>
</div>