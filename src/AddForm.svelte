
<style>
.btn {
  color: white;
  padding: 15px 20px;
  border: none;
  cursor: pointer;
  width: 48%;
  opacity: 0.9;
}
.btn-main{
  background-color: dodgerblue;
  margin-left:2%
}
.btn-cancel{
  background-color: #bb2727;
  margin-right:2%;
}
.input-field {
  width: 100%;
  padding: 10px;
  outline: none;
}
.input-field:focus {
  border: 2px solid dodgerblue;
}
.btn:hover {
  opacity: 1;
}
.flex{
display:flex;
}
</style>

<script>
   export let toggleView
   export let formType
    export let first=''
    export let last=''
    export let age=''
    export let id =''
    export let AddPerson
    console.log(first)
    function handleSubmit(){
      let data = {
        first: first,
        last: last,
        age:age
      }
      AddPerson(data, formType, id)
    }
    function cancelForm(){
        first=''
        last=''
        age=''
      toggleView()
    }
</script>

<form on:submit|preventDefault={handleSubmit} autocomplete="off">
  <h2>{formType === 'EDIT'? 'Update person details':'Add person details'}</h2>
  <div>
    <input class="input-field" type="text" bind:value={first} placeholder="First Name" name="fname" >
  </div>

  <div>
    <input class="input-field" type="text" bind:value={last} placeholder="Last Name" name="lname">
  </div>

  <div>
    <input class="input-field" type="number" bind:value={age} placeholder="age" name="age">
  </div>
    <div class="flex">
    <button type="button" class="btn btn-cancel" on:click={cancelForm}>Cancel</button>
    <button type="submit" class="btn btn-main" disabled="{!first || !last || !age}">{formType === 'EDIT'? 'Update':'Add person'}</button>
  </div>
</form>