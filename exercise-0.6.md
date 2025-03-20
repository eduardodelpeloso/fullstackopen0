```mermaid
sequenceDiagram
  participant browser as browser
  participant server as server

  browser ->>+ server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
  Note right of browser: This is the only request made to the server in the single-page app;
  Note right of browser: The payload is JSON data containing the text of the new note and a timestamp
  Note right of server: When the browser receives the POST request it appends the new note to the JSON file
  server -->>- browser: HTTP status code 201
  Note right of browser: This means "created" and no instruction is sent to the browser to request any page
  Note right of browser: The Javascript file sent by the server when the page was first accessed now updates the
  Note right of browser: local JSON file with the new note and renders the new page
