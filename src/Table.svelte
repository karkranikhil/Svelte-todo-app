<script>
	export let persons;
    export let AddPerson;
    export let editCallback;
    export let deleteCallback;
    let textValue = '';
    console.log(persons)
    /*filter logic*/
        $: filteredPersons = textValue
		? persons.filter(person => {
			const name = `${person.last}, ${person.first}`;
			return name.toLowerCase().includes(textValue.toLowerCase());
		})
		: persons;
    /*filter logic end*/

    /*Edit person logic*/
        function editPerson(person){
               editCallback(person)
        }
    /*Edit person logic end*/

    /*delete person logic start*/
        function deletePerson(person){
               deleteCallback(person)
        }
    /*delete person logic end*/
</script>

<style>
#myInput {
  background-position: 10px 12px;
  background-repeat: no-repeat; 
  width: 100%; 
  font-size: 16px;
  padding: 12px 20px 12px 20px; 
  border: 1px solid #ddd; 
  margin-bottom: 12px;
  margin-top: 12px;
}

#myTable {
  border-collapse: collapse; 
  width: 100%;
  border: 1px solid #ddd;
  font-size: 18px; 
  
}

#myTable th, #myTable td {
  text-align: left; 
  padding: 12px; 
}

#myTable tr {
  border-bottom: 1px solid #ddd; 
}

#myTable tr.header, #myTable tr:hover {
  background-color: #f1f1f1;
}
.icon{
    width:50px;
        padding-right: 2rem;
}
.cursor{
  cursor:pointer;
}
</style>


<input id="myInput" type="text" bind:value={textValue} placeholder="Search by first name and last name.">

<table id="myTable">
  <tr class="header">
    <th style="width:30%;">First Name</th>
    <th style="width:30%;">Last Name</th>
    <th style="width:30%;">Age</th>
    <th style="width:10%;">Actions</th>
  </tr>
  {#each filteredPersons as person, i}
    <tr>
        <td>{person.first}</td>
        <td>{person.last}</td>
        <td>{person.age}</td>
        <td>
            <span class="icon" on:click={()=>editPerson(person)} ><i class="fas fa-edit cursor"></i></span>
            <span class="icon" on:click={()=>deletePerson(person)} ><i class="fas fa-trash cursor"></i></span>
        </td>
    </tr>
   {/each}
</table>