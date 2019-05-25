<script>
import AddForm from './AddForm.svelte'
    import Table from './Table.svelte'
    let persons = [
		{   
            id:1,
			first: 'Joe',
			last: 'Doe',
			age:23
		},
		{   
            id:2,
			first: 'John',
			last: 'Smith',
			age:25
		},
		{   
            id:3,
			first: 'David',
			last: 'Martin',
			age:28
		}
	];
    let initialValue ={
			first: '',
			last: '',
			age:'',
            id:''
    }
    let showTable = true
    let personValue={}
    let formType ='CREATE'
	function toggleView() {
		showTable = !showTable
	}

    function generateId() {
        return '_' + Math.random().toString(36).substr(2, 9);
    };

    function AddPerson(data, type, index) {
        
        if(type === 'EDIT'){
            data.id=index
            const objIndex = persons.findIndex(obj => obj.id === index);
            persons[objIndex]=data
            toggleView()
        } else {
            let newPerson = {...data,id:generateId()}
            persons.push(newPerson)
            toggleView()
        }
    }

    function editCallback(person){
        personValue = persons.filter(item=>item.id === person.id)
        formType="EDIT"
        toggleView()
    }

    function deleteCallback(person) {
         persons =persons.filter(item=>item.id!=person.id)
	}

</script>

<style>
.btn {
  background-color: dodgerblue;
  color: white;
  padding: 15px 20px;
  border: none;
  cursor: pointer;
  float: right;
  margin-top: 10px;
  opacity: 0.9;
}
</style>

{#if !showTable}
    {#if formType=== 'CREATE'}
        <AddForm formType={formType} {...initialValue} AddPerson={AddPerson} toggleView={toggleView}/>
    {:else}
        <AddForm formType={formType} {...personValue[0]} AddPerson={AddPerson} toggleView={toggleView}/>
    {/if}
{/if}

{#if showTable}
    <button class="btn" on:click={toggleView}>Add Person</button>
	<Table persons={persons} deleteCallback={deleteCallback} editCallback={editCallback}/>
{/if}


