<script>
	import NotePlaceholder from './NotePlaceholder.svelte';
	import Note from './Note.svelte';
    export let notes


</script>

<div class="Dashboard">

    <div class="notes-container">
        <NotePlaceholder on:click/>
        {#each notes as {id, title, color, text} }
        <Note {id} bind:title={title} {color} bind:text={text} on:update on:color on:remove/>
        {/each}
    </div>


</div>


<style>
    .Dashboard {
        margin: 0 auto;
        width: calc(100vw - 3rem);
        min-height: calc(100vh - 15rem);
        padding: 20px;
        background-image: url(../assets/img/cork2.jpg);
        box-shadow: 7px 55px 52px -3px rgba(0,0,0,0.31);
}
    
    .notes-container {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        width: 100%;
        gap: 10px
    }

</style>