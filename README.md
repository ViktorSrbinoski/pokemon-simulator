# pokemon-simulator

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```
This is a simplified pokemon battle simulator. It will calculate how much damage two pokemon will deal to each other using specified moves.
Things considered when calculating damage: type matchup, relevant attack and defence stats, move power, Same Type Attack Bonus (STAB), and a random variance of power (from 85% to 100%)
Things not considered: pokemon IVs/EVs/Natures, stat boosts/drops, ailments/statuses, screens, weather/terrain effects and critical hit chance.
In order to use simply pick two pokemon from the first two dropdowns, then choose which move each pokemon will use (again with the relevant dropdowns) and hit battle.

To start the pokemon simulator simply run "npm run serve", and the service will start on port 8080
This service will work locally without also cloning and starting the backend server, as it's querying a heroku instance. This behavior can be changed by changing the "serverHost" variable in the PokemonSimulator.vue file to "http://localhost:9990". This will now point to the local instance of the python FastApi)