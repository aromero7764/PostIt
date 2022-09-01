<script>
	import Header from './Header.svelte';
	import Note from './Note.svelte';

export let title;
export let color;   
export let text;  
export let id;
import { createEventDispatcher } from 'svelte'

const dispatch = createEventDispatcher();

const  handleChange = ()=> {
    dispatch ('update', {
        id: id,
        title: '',
        color: color,
        text: '',
    })
}

const  handleColor = ()=> {
    dispatch ('color', {
        id: id,
       
    })
}

const  handleRemove = ()=> {
    dispatch ('remove', {
        id: id,
       
    })
}


</script>

<div class="Note">
   <div class="Note-container" style={'background-color:' + color}>
            <div class="header">
                <div class="options">
                    <button on:click={handleColor}><span class="material-symbols-outlined">
                        palette
                        </span></button>
                    <button on:click={handleRemove}><span class="material-symbols-outlined">
                        delete
                        </span></button>
                </div>
            </div>
            <div class="content">
                        <div class="title">
                        <input type="text" placeholder="Title..." bind:value={title} >
                        </div>
                        <div class="text">
                        <textarea 
                        bind:value={text} 
                            cols="30" 
                            rows="10" 
                            placeholder="Add a note..." 
                            ></textarea>
                        </div>
            </div> 
        

   </div>
</div>


<style>
   .Note {
        background-color: whitesmoke;
        border-radius: 3px;
        border: solid 2px transparent;
        overflow: hidden;
        height: 272px;
        width: 309px;
        box-shadow: 11px 13px 15px -3px rgba(0,0,0,0.23);
    }
   .Note-container {
        height: 100%;
    }
    .Note:focus-within {
        border: solid 2px black;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    }
    
    .Note .Note-container .header {
        padding: 5px;
    }

    .header .options {
        display: flex;
        justify-content: space-between;
    }
    .Note .content {
        padding: 0 20px;
    }

    .text textarea {
        width: 100%;
        border: 0;
        outline: none;
        resize: none;
        height: 250px;

    }
    .title input {
        font-size: 22px;
        font-weight: bold;
        padding: 10px;
        outline: none;
        border: none;
        width: 100%;
    } 
    button {
        margin: 0;
        border: none;
        background-color: transparent;
        cursor: pointer;
    }

    textarea, input {
        background-color: transparent;
    }

  
.material-symbols-outlined {
  font-variation-settings:
  'FILL' 0,
  'wght' 400,
  'GRAD' 0,
  'opsz' 48
}


</style>

