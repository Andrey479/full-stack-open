'''mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    server-->>browser: 302 Found (Redirect to /notes)
    deactivate server

    Note right of browser: Navegador segue o redirect

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML (notes page)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON data (notas atualizadas)
    deactivate server

    Note right of browser: Browser renderiza a página com a nova nota

sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML (single page)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: JavaScript file (spa.js)
    deactivate server

    Note right of browser: JavaScript executa e faz fetch dos dados

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON data (notas iniciais)
    deactivate server

    Note right of browser: Browser renderiza as notas dinamicamente via JS

sequenceDiagram
    participant browser
    participant server

    Note over browser: Usuário digita nota e clica submit

    browser->>browser: JavaScript intercepta submit (preventDefault)

    browser->>browser: Cria nota localmente e atualiza lista na tela

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server
    Note right of browser: Envia dados como JSON {content: "...", date: "..."}
    server-->>browser: 201 Created (sem redirect)
    deactivate server

    Note right of browser: Página continua a mesma, nota já aparece (JS atualizou DOM)