# Fullstack-Open-Part0
Exercise submissions for part 0
https://fullstackopen.com/en/part0/fundamentals_of_web_apps#exercises-0-1-0-6

> ## Exercises 0.1 - 0.6
The exercises are submitted via GitHub, and by marking the exercises as done in the submission application.

You can submit all of the exercises into the same repository, or use multiple different repositories. If you submit exercises from different parts into the same repository, name your directories well. If you use a private repository to submit the exercises, add mluukkai as a collaborator to it.

One good way to name the directories in your submission repository is as follows:
```bash
part0
part1
    courseinfo
    unicafe
    anecdotes
part2
    courseinfo
    phonebook
    countries
```
So, each part has its own directory, which contains a directory for each exercise set (like the unicafe exercises in part 1).

The exercises are submitted **one part at a time**. When you have submitted the exercises for a part, you can no longer submit any missed exercises for that part.

## Exercise 0.1: HTML
> Review the basics of HTML by reading this tutorial from Mozilla: [HTML tutorial](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics).

## Exercise 0.2: CSS
> Review the basics of CSS by reading this tutorial from Mozilla: [CSS tutorial](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics).

## Exercise 0.3: HTML Forms
> Learn about the basics of HTML forms by reading Mozilla's tutorial [Your first form](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Your_first_HTML_form).

## Exercise 0.4: New note diagram
> In the section [Loading a page containing Javascript - review](https://fullstackopen.com/en/part0/fundamentals_of_web_apps#loading-a-page-containing-java-script-review), the chain of events caused by opening the page https://studies.cs.helsinki.fi/exampleapp/notes is depicted as a [sequence diagram](https://www.geeksforgeeks.org/unified-modeling-language-uml-sequence-diagrams/)
> The diagram was made as a GitHub Markdown-file using the [Mermaid](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams)-syntax as follows:

```bash
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
```
> **Create a similar diagram** depicting the situation where the user creates a new note on the page https://studies.cs.helsinki.fi/exampleapp/notes by writing something into the text field and clicking the Save button.
> 
> If necessary, show operations on the browser or on the server as comments on the diagram.
> 
> The diagram does not have to be a sequence diagram. Any sensible way of presenting the events is fine.
> 
> All necessary information for doing this, and the next two exercises, can be found in the text of [this part](https://fullstackopen.com/en/part0/fundamentals_of_web_apps#forms-and-http-post). The idea of these exercises is to read the text once more and to think through what is going on there. Reading the application [code](https://github.com/mluukkai/example_app) is not necessary, but it is of course possible.
> 
> You can do the diagrams with any program, but perhaps the easiest and the best way to do diagrams is the [Mermaid](https://github.com/mermaid-js/mermaid#sequence-diagram-docs---live-editor) syntax that is now implemented in [GitHub](https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/) Markdown pages!  

# Solution!
```mermaid
sequenceDiagram
	participant browser
	participant server

	browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
	activate server
	server-->>browser: 302 Found 
	deactivate server

  	Note right of browser: HTTP Status Code 302: (This is a response code from the server which asks the browser to do a redirect or a new HTTP GET request 	to the address in the header)

  	browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
	activate server
	server-->>browser: notes.html (HTML file)
	deactivate server

  	browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
	activate server
	server-->>browser: main.css (CSS file) 
	deactivate server

  	browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
	activate server
	server-->>browser: main.js (JS file)
	deactivate server

  	Note over browser: The browser starts executing the JS code which requests the data.json file from the server

  	browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
	activate server
	server->>browser: [{content: “HTML is easy”, date: “2019-05-23”}, …]
	deactivate server

  	Note over browser: The browser executes the callback function that renders the notes
```

## Exercise 0.5: Single page app diagram
> Create a diagram depicting the situation where the user goes to the single-page app version of the notes app at https://studies.cs.helsinki.fi/exampleapp/spa.

# Solution!
```mermaid
sequenceDiagram
	participant browser
	participant server

	browser->>server: GET https://https://studies.cs.helsinki.fi/exampleapp/spa
	activate server
	server-->>browser: spa.html (HTML File)
	deactivate server

	browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
	activate server
	server-->>browser: main.css (CSS File)
	deactivate server

	browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
	activate server
	server-->>browser: spa.js (JS File)
	deactivate server

	Note over browser: The browser starts executing the JavaScript code that fetches the JSON from the server

	browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
	activate server
	server->>browser: [{content: “HTML is easy”, date: “2019-05-23”}, …]
	deactivate server

	Note over browser: The browser executes the callback function that renders the notes
```

## Exercise 0.6: New note in Single page app diagram
> Create a diagram depicting the situation where the user creates a new note using the single-page version of the app.
>
> This was the last exercise, and it's time to push your answers to GitHub and mark the exercises as done in the [submission system](https://studies.cs.helsinki.fi/stats/courses/fullstackopen).

# Solution!
```mermaid
sequenceDiagram
	participant browser
	participant server

	Note Left of browser: The browser pushes the new note data on the existing notes and rerenders only the notes list instead of the entire page

	browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
	activate server

	Note Over browser: The browser sends the new note list as JSON to the server

	server-->>browser: {"message":"note created"}
	deactivate server

	Note Over server: The server processes the post request and responds with 201 code and new_note_spa.json
```
