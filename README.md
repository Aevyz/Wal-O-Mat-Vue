# quiz

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

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### Data Structure

```$xslt
- Question[]
-- ID
-- Text

- Party[]
-- Name
-- Response[]
--- Question.ID
--- Response
```

### Translations
https://www.codeandweb.com/babeledit/tutorials/how-to-translate-your-vue-app-with-vue-i18n