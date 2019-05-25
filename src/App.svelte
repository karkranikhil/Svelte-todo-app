<script>
	import Navbar from './Navbar.svelte';
	import Todo from './Todo.svelte';
	export let name;
	
</script>

<style>
.container{
	padding:2rem;
}
</style>


<Navbar heading="Svelte 3 - Compile-time framework"/>
<div class="container">
<Todo/>
</div>
