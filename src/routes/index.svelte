<script>
	import supabase from "$lib/db";

    async function signOut() {
   	 const { error } = await supabase.auth.signOut();

   	 if (error) alert(error.message); // alert if error
    }

	async function getEntries() {
		const { data, error } = await supabase.from("studentEntries").select();
		if (error) alert(error.message);

		if (data != "") {
			timetable = data[0].timetable;
		}
	}

	getEntries();
	
	 let timetable = {
	Monday: [
  	{
    	name: "PH",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "PM",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "BI",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "R",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "M3",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "BC",
    	period: 2,
    	style: "",
  	},
	],
	Tuesday: [
  	{
    	name: "PJPK",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "M3",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "BI",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "E",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "BC",
    	period: 3,
    	style: "",
  	},
  	{
    	name: "PJPK",
    	period: 1,
    	style: "",
  	},
	],
	Wednesday: [
  	{
    	name: "BC",
    	period: 3,
    	style: "",
  	},
  	{
    	name: "PM",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "H",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "PKS",
    	period: 3,
    	style: "",
  	},
  	{
    	name: "BM",
    	period: 3,
    	style: "",
  	},
	],
	Thursday: [
  	{
    	name: "SA",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "PJPK",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "A",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "PM",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "BC",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "M3",
    	period: 3,
    	style: "",
  	},
	],
	Friday: [
  	{
    	name: "BI",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "T",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "BC",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "PM",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "SA",
    	period: 3,
    	style: "",
  	},
	],
  };

      
let curDay;
let	curIndex;
let curName;
let	curPeriod;
let	curStyle;

function showCurData(day, index, name, period, style){
	curDay=day;
	curIndex=index;
	curName=name;
	curPeriod=period;
	curStyle=style;
}

	function setTimeslot(day, index, newName, newPeriod, newStyle){
		if (day === "Monday") {
  			timetable.Monday[index].name = newName;
  			timetable.Monday[index].period = newPeriod;
  			timetable.Monday[index].style = newStyle;
		}
		else if (day === "Tuesday") {
  			timetable.Tuesday[index].name = newName;
  			timetable.Tuesday[index].period = newPeriod;
  			timetable.Tuesday[index].style = newStyle;
		}
		else if (day === "Wednesday") {
  			timetable.Wednesday[index].name = newName;
  			timetable.Wednesday[index].period = newPeriod;
  			timetable.Wednesday[index].style = newStyle;
		}
		else if (day === "Thursday") {
  			timetable.Thursday[index].name = newName;
  			timetable.Thursday[index].period = newPeriod;
  			timetable.Thursday[index].style = newStyle;
		}
		else {
  			timetable.Friday[index].name = newName;
  			timetable.Friday[index].period = newPeriod;
  			timetable.Friday[index].style = newStyle;
		}
		saveEntry();
	}

	async function saveEntry() {
		const { error } = await supabase.from("studentEntries").upsert(
				{
				user_id: supabase.auth.user().id,
				timetable: timetable,
				},
			{onConflict: "user_id" }
		);
	if (error) alert(error.message);
	}


	function deleteTimeSlot(day,index) {
		if (day === "Monday") {
  			timetable.Monday.splice(index, 1);
  			timetable = timetable;
		}
		else if (day === "Tuesday") {
  			timetable.Tuesday.splice(index, 1);
  			timetable = timetable;
		}
		else if (day === "Wednesday") {
  			timetable.Wednesday.splice(index, 1);
  			timetable = timetable;
		}
		else if (day === "Thursday") {
  			timetable.Thursday.splice(index, 1);
  			timetable = timetable;
		}
		else {
  			timetable.Friday.splice(index, 1);
  			timetable = timetable;
		}
		saveEntry();
	}


   

function addTimeSlot(day){
	if (day=="Monday"){
		 timetable.Monday = [
    		...timetable.Monday,
    		{ name: "??", period: 1, style: "" }
  ];
	}
	else if(day=="Tuesday"){
		timetable.Tuesday = [
    		...timetable.Tuesday,
    		{ name: "??", period: 1, style: "" }
		];
	}
	else if(day=="Wednesday"){
		timetable.Wednesday = [
    		...timetable.Wednesday,
    		{ name: "??", period: 1, style: "" }
			];
	}
	else if(day=="Thursday"){
		timetable.Thursday = [
    		...timetable.Thursday,
    		{ name: "??", period: 1, style: "" }
			];
	}
	else{
		timetable.Friday = [
    		...timetable.Friday,
    		{ name: "??", period: 1, style: "" }
			];
	}
}

      
</script>
<h1>My dashboard</h1>
<h4>My school time-table </h4>
<table class="table text-center table-bordered">
  <thead>
    <tr class="table-dark">
      <th scope="col">#</th>
      <th scope="col">1</th>
      <th scope="col">2</th>
      <th scope="col">3</th>
      <th scope="col">4</th>
      <th scope="col">-</th>
      <th scope="col">5</th>
      <th scope="col">6</th>
      <th scope="col">7</th>
      <th scope="col">8</th>
      <th scope="col">9</th>
      <th scope="col">10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Monday</th>
      {#each timetable.Monday as timeSlot,index}
        <td colspan={timeSlot.period} class={timeSlot.style}>
        <button class="btn" type="button" data-bs-toggle="modal" data-bs-target="#editTimeSlot" on:click={() =>
			showCurData(
			  "Monday",
			  index,
			  timeSlot.name,
			  timeSlot.period,
			  timeSlot.style
			)}
> {timeSlot.name}</button>
        </td>
        
      {/each}
	  	<td class="btn" on:click={() => addTimeSlot("Monday")}>+</td>
    </tr>
    <tr>
      <th scope="row">Tuesday</th>
      {#each timetable.Tuesday as timeSlot,index}
        <td colspan={timeSlot.period} class={timeSlot.style}>
         <button class="btn" type="button" data-bs-toggle="modal" data-bs-target="#editTimeSlot" on:click={() =>
			showCurData(
			  "Tuesday",
			  index,
			  timeSlot.name,
			  timeSlot.period,
			  timeSlot.style
			)}
> {timeSlot.name}</button>
        </td>
       
      {/each}
	  	<td class="btn" on:click={() => addTimeSlot("Tuesday")}>+</td>
    </tr>
    <tr>
      <th scope="row">Wednesday</th>
      {#each timetable.Wednesday as timeSlot,index}
        <td colspan={timeSlot.period} class={timeSlot.style}>
         <button class="btn" type="button" data-bs-toggle="modal" data-bs-target="#editTimeSlot"
		on:click={() =>
			showCurData(
			  "Wednesday",
			  index,
			  timeSlot.name,
			  timeSlot.period,
			  timeSlot.style
			)}
> {timeSlot.name}</button>
        </td>
       
      {/each}
	  	<td class="btn" on:click={() => addTimeSlot("Wednesday")}>+</td>
    </tr>
    <tr>
      <th scope="row">Thursday</th>
      {#each timetable.Thursday as timeSlot,index}
        <td colspan={timeSlot.period} class={timeSlot.style}>
         <button class="btn" type="button" data-bs-toggle="modal" data-bs-target="#editTimeSlot"
		 on:click={() =>
			showCurData(
			  "Thursday",
			  index,
			  timeSlot.name,
			  timeSlot.period,
			  timeSlot.style
			)}
> {timeSlot.name}</button>
        </td>
       
      {/each}
	  	<td class="btn" on:click={() => addTimeSlot("Thursday")}>+</td>
    </tr>
    <tr>
      <th scope="row">Friday</th>
     {#each timetable.Friday as timeSlot,index}
        <td colspan={timeSlot.period} class={timeSlot.style}>
         <button class="btn" type="button" data-bs-toggle="modal" data-bs-target="#editTimeSlot" on:click={() =>
			showCurData(
			  "Friday",
			  index,
			  timeSlot.name,
			  timeSlot.period,
			  timeSlot.style
			)}
> {timeSlot.name}</button>
        </td>
       
      {/each}
	  	<td class="btn" on:click={() => addTimeSlot("Friday")}>+</td>
    </tr>
  </tbody>
</table>

<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
    <button class="btn btn-secondary" on:click={signOut}>Logout</button>
</section>


<!-- Modal -->
<div class="modal fade" id="editTimeSlot" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Edit Time Slot</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
		<div class="input-group mb-3">
  			<span class="input-group-text" id="basic-addon1">Name</span>
 			<input type="text" class="form-control" placeholder="Acronym of subject" aria-label="Username" aria-describedby="basic-addon1" bind:value={curName}>
		</div>
		<div class="input-group mb-3">
  			<span class="input-group-text" id="basic-addon1">Period</span>
 			<input type="number" class="form-control" placeholder="Period no." aria-label="Username" aria-describedby="basic-addon1" bind:value={curPeriod}>
		</div>
		<div class="input-group mb-3">
  			<span class="input-group-text" id="basic-addon1">Style</span>
 			<select class="form-select"  id="inputGroupSelect01" bind:value={curStyle}>
    			<option selected value>Default</option>
    			<option value="table-primary">Blue</option>
    			<option value="table-success">Green</option>
    			<option value="table-danger">Red</option>
				<option value="table-warning">Yellow</option>
				<option value="table-secondary">Grey</option>
  			</select>
		</div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
		<button type="button" class="btn btn-danger"	data-bs-dismiss="modal" on:click={() => deleteTimeSlot(curDay, curIndex)}>Delete</button>
        <button type="button" class="btn btn-primary" on:click=
		{
		()=>{setTimeslot(curDay,curIndex,curName,curPeriod,curStyle)}} >Save changes</button>
      </div>
    </div>
  </div>
</div>