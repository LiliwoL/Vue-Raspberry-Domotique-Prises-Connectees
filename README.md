# vue-raspberry-prises-connectees

Frontend pour le projet Raspberry

A faire correspondre à

https://github.com/LiliwoL/Python-Raspberry-Domotique-Prises-Connectees

## Configuration

Dans un fichier **.env** spécifiez les champs:

```env
# API Endpoint
VUE_APP_API_ENDPOINT=http://192.168.1.56/api

# Api endpoint suffix to switch
VUE_APP_API_SWITCH_URL=/switch/

# Api endpoint suffix to init and get switches states
VUE_APP_API_INIT_URL=/init/

# API Key
VUE_APP_API_KEY=raspB3rr1
```

***

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
