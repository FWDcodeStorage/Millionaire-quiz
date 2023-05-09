# mermaid diagram
..first try

```mermaid
flowchart LR;
setup dev(Setup)
participant browser
participant server
A [browser]--> B [server:] 
C [GET https://studies.cs.helsinki.fi/exampleapp/notes]
    
```

# quiz-game

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
