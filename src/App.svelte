<script>
import Dashboard from "./components/Dashboard.svelte"
import Header from "./components/Header.svelte"
import {v4} from "uuid";
import Note from "./components/Note.svelte";

  let notes = [
    {
      id: 0,
      title: 'Birthday of Nian',
      color: 'Yellow',
      text: 'october 23th, buy a gift '
    },
    {
      id: 1,
      title: 'Appointment ',
      color: 'Red',
      text: 'Dr. House October 25th'
    }
]
let copyNotes = [...notes]
$: count = notes.length

const generateColor = ()=> {
  const colors = ["#ff0000","#ff9a00", "#d0de21", "#4fdc4a", "#3fdad8", "#2fc9e2", "#1c7fee", "#5f15f2", "#ba0cf8", "#fb07d9"]
  const index = Math.floor(Math.random() * (colors.length))
  return colors[index]
}

const handleNew = ()=> {
  const color = generateColor();
  const id = v4()
  const note = {
    id: id,
    title: '',
    color: color,
    text: ''
  }
  notes = [note,... notes]
  copyNotes = [...notes]

}

const handleUpdate = (e)=> {
  const note = e.detail
  const index = notes.findIndex(n => n.id === note.id)
  notes[index] = note;
  copyNotes = [...notes]
}

const handleColor = (e)=> {
  const index = notes.findIndex(n => n.id === e.detail.id)
  notes[index].color = generateColor();
  copyNotes[index].color = notes[index].color
}

const handleRemove = (e)=> {
  const response = notes.filter(n => n.id !== e.detail.id)
  notes = [...response]
  copyNotes = [...notes] 
 
}

const handleSearch = (e) => {
  
  const q = e.target.value.toLocaleLowerCase();
    if(q === '') {
      copyNotes = [...notes];
      return false
    }

    const result = notes.filter(note => {
        const title = note.title.toLocaleLowerCase();
        const text = note.text.toLocaleLowerCase();
        return title.indexOf(q) > -1 || text.indexOf(q) > -1;
    })
    copyNotes = [...result];
}


</script>

<main>
  <div class="box">
    <div class="count-notes is-size-3 has-text-weight-semibold"><span class="material-symbols-outlined">
      save
      </span>{count} Post It</div>
    <div><Header on:input={handleSearch}/></div>
  </div>

<Dashboard 
      bind:notes={copyNotes} 
      on:click={handleNew} 
      on:update={handleUpdate} 
      on:color={handleColor}
      on:remove={handleRemove}
      />
    
</main>

<style>
  

.box{
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  padding-top: 10px;
  opacity: 0.8;
}


main {
  min-height: 100vh;
  background-image: linear-gradient(to right top, #b0c4e1, #64d1f3, #00ddd9, #20e18f, #9fd81e);
}

.material-symbols-outlined{
font-size: 35px;

}
  
</style>

