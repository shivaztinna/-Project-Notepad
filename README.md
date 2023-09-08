#Project-Notepad
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Notepad</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        text-align: center;
      }
      #notes-container {
        max-width: 400px;
        margin: 0 auto;
      }
      .note {
        border: 1px solid #ccc;
        padding: 10px;
        margin: 10px 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }
      .delete-button {
        background-color: #ff4444;
        color: white;
        border: none;
        padding: 5px 10px;
        cursor: pointer;
      }
      .delete-button:hover {
        background-color: #cc0000;
      }
    </style>
  </head>
  <body>
    <h1>Notepad</h1>
    <div id="notes-container">
      <div id="note-list"></div>
      <textarea id="note-text" placeholder="Enter your note..."></textarea>
      <button onclick="saveNote()">Save</button>
    </div>

    <script>
      // Load existing notes from local storage
      function loadNotes() {
        const notes = JSON.parse(localStorage.getItem("notes")) || [];
        const noteList = document.getElementById("note-list");

        noteList.innerHTML = "";

        notes.forEach((note, index) => {
          const noteDiv = document.createElement("div");
          noteDiv.classList.add("note");
          noteDiv.innerHTML = `
                      <div>${note}</div>
                      <button class="delete-button" onclick="deleteNote(${index})">Delete</button>
                  `;
          noteList.appendChild(noteDiv);
        });
      }

      // Save a new note to local storage
      function saveNote() {
        const noteText = document.getElementById("note-text").value;
        if (noteText.trim() === "") return;

        const notes = JSON.parse(localStorage.getItem("notes")) || [];
        notes.push(noteText);
        localStorage.setItem("notes", JSON.stringify(notes));

        loadNotes();
        document.getElementById("note-text").value = "";
      }

      // Delete a note from local storage
      function deleteNote(index) {
        const notes = JSON.parse(localStorage.getItem("notes")) || [];
        notes.splice(index, 1);
        localStorage.setItem("notes", JSON.stringify(notes));
        loadNotes();
      }

      // Initial load of notes
      loadNotes();
    </script>
  </body>
</html>
