# Scrimba Notes App project with React & NodeJs

## Screenshot
![notes-screenshot](https://user-images.githubusercontent.com/109000703/191743325-3efb27f6-176c-4375-beb9-d72dada494c6.png)


## Built With
- HTML5
- CSS / Flexbox
- React.js
- Node.js

## What I Learned
- Sync Notes to localStorage 
```
const [notes, setNotes] = React.useState(
      () => JSON.parse(localStorage.getItem("notes")) || []
  );
  const [currentNoteId, setCurrentNoteId] = React.useState(
      (notes[0] && notes[0].id) || ""
  );
  React.useEffect(() => {
      localStorage.setItem("notes", JSON.stringify(notes))
  },  [notes]);
```
- Add note summary titles
```
 const noteElements = props.notes.map((note, index) => (
        <div key={note.id}>
            <div
                className={`title ${
                    note.id === props.currentNote.id ? "selected-note" : ""
                }`}
                onClick={() => props.setCurrentNoteId(note.id)}
            > 
                <h4 className="text-snippet">{note.body.split("\n")[0]}</h4>
```
- Move modified notes to top of the list  
```
function updateNote(text) {
      setNotes(oldNotes => {
        //modified note to top of list
        const newArray = []
        for(let i = 0; i < oldNotes.length; i++) {
            const oldNote = oldNotes[i]
            if(oldNote.id === currentNoteId) {
                newArray.unshift({ ...oldNote, body: text })
            } else {
                newArray.push(oldNote)
            }
        }
        return newArray
      });
  }
```
- Delete Notes
```
function deleteNote(event, noteId) {
    event.stopPropagation()
    // only delete note clicked
    setNotes(oldNotes => oldNotes.filter(note => note.id !== noteId))
  }
```

