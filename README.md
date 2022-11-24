# pokemon-simulator

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

To start the pokemon simulator simply run "npm run serve", and the service will start on port 8080
This service will work locally without also cloning and starting the backend server, as it's querying a heroku instance. This behavior can be changed by changing the "serverHost" variable in the PokemonSimulator.vue file to "http://localhost:9990". This will now point to the local instance of the python FastApi)