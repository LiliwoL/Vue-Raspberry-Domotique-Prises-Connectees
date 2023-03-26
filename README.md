# Gestion des prises connectées sur un Raspberry

Frontend pour le projet Raspberry https://github.com/LiliwoL/Python-Raspberry-Domotique-Prises-Connectees

Une application Frontend pour communiquer avec l'API placée sur le raspberry.

![](readme_docs/home.png)

## Configuration

Dans un fichier **.env.local** spécifiez les champs:

```env
# API Endpoint
VUE_APP_API_ENDPOINT=http://192.168.1.56/api

# Api endpoint suffix to switch
VUE_APP_API_SWITCH_URL=switch/

# Api endpoint suffix to init and get switches states
VUE_APP_API_INIT_URL=/init/

# API Key
VUE_APP_API_KEY=raspB3rr1
```

***

## Installation des dépendances
```bash
npm install
```

## Version de développement
```bash
npm run serve
```

## Compilation pour déploiement
```bash
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
