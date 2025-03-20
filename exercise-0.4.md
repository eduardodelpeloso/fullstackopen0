```mermaid
sequenceDiagram
  participant browser as browser
  participant server as server

  browser ->>+ server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
  Note right of browser: The data sent by the POST request (the "payload") is the text of the new note
  Note right of browser: The payload type is indicated by the Content-Type header, in our case text/html using the utf-8 charset
  Note right of server: When the browser receives the POST request it appends the new note to the JSON file
  server -->>- browser: HTTP status code 302
  Note right of browser: This is a URL redirect that prompts the browser to reload the notes page
  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/notes
  server -->>- browser: the HTML file
  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
  server -->>- browser: the CSS file
  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
  server -->>- browser: the Javascript file
  Note right of browser: The browser starts executing the JavaScript code that fetches the JSON file from the server
  browser ->>+ server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
  server -->>- browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
  Note right of browser: The browser executes the callback function that renders the notes
  Note right of browser: Mark that the downloaded JSON file already contains the new note text, that was added by the server
