<script>

    async function signOut() {
   	 const { error } = await supabase.auth.signOut();

   	 if (error) alert(error.message); // alert if error
    }

    // Select entries
    async function getEntries() {
   	 const { data, error } = await supabase.from('moodEntries').select();
   	 if (error) alert(error.message);

   	 return data;
    
      let timetable = {
	Monday: [{
     	name: "PH", //Perhimpunan (Morning Assembly)
     	period: 1,
     	style: "",
   	},
   	{
     	name: "PM", // Pendidikan Moral (Moral Studies)
     	period: 1,
     	style: "",
   	},
   	{
     	name: "BI", // Bahasa Inggeris (English Subject)
     	period: 2,
     	style: "",
   	},
],
	Tuesday: [],
	Wednesday: [],
	Thursday: [],
	Friday: [],
  };
    }
</script>
<h1>My dashboard</h1>
<h4>My school time-table </h4>
<table class="table table-dark">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">1</th>
      <th scope="col">2</th>
      <th scope="col">3</th>
      <th scope="col">4</th>
      <th scope="col">5</th>
      <th scope="col">6</th>
      <th scope="col">7</th>
      <th scope="col">8</th>
      <th scope="col">9</th>
      <th scope="col">10</th>
      <th scope="col">11</th>
      <th scope="col">12</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Monday</th>
      {#each timetable.Monday as timeSlot,index}
      <td colspan="{timeSlot.period}" class="{timeSlot.style}"></td>
      </each>
    </tr>
    <tr>
      <th scope="row">Tuesday</th>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">Wednesday</th>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">Thursday</th>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th scope="row">Friday</th>
      <td colspan="2"></td>
      <td></td>
    </tr>
  </tbody>
</table>

<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
    <button class="btn btn-secondary" on:click={signOut}>Logout</button>
</section>
