<template>
    <div class="central_container">
        <div class="image_container">
            <select @change="updatePokemon1" v-model="pokemon1" class="pokemon_select">
                <option v-for="pokemon in allPokemon" :value="pokemon.name" :key="pokemon">{{pokemon.name}}</option>
            </select>
            <img v-bind:src="pokemon1Image" alt="select pokemon">
            <div class="stats">
                HP:
                <progress :value="pokemon1HP" max="255"></progress>
            </div>
            <div class="stats">
                Attack:
                <progress :value="pokemon1Attack" max="190"></progress>
            </div>
            <div class="stats">
                Defence:
                <progress :value="pokemon1Defence" max="250"></progress>
            </div>
            <div class="stats">
                Sp. Attack:
                <progress :value="pokemon1SpAtt" max="194"></progress>
            </div>
            <div class="stats">
                Sp. Defence:
                <progress :value="pokemon1SpDef" max="250"></progress>
            </div>
            <div class="stats">
                Speed:
                <progress :value="pokemon1Speed" max="200"></progress>
            </div>
            <hr/>
            <div class="hp_div">
                <div class="hp_text"> Current HP:</div>
                <progress :value="pokemon1CurrentHP" :max="pokemon1HP" class="main_hp"></progress>
                <div class="hp_text"> {{pokemon1CurrentHP}} / {{pokemon1HP}}</div>
            </div>
            <p>Choose attacking move</p>
            <select @change="updateMove1" v-model="move1" class="pokemon_select">
                <option v-for="move in allMoves" :value="move.name" :key="move">{{move.name}}</option>
            </select>
        </div>
        <div class="image_container">
            <select @change="updatePokemon2" v-model="pokemon2" class="pokemon_select">
                <option v-for="pokemon in allPokemon" :value="pokemon.name" :key="pokemon">{{pokemon.name}}</option>
            </select>
            <img v-bind:src="pokemon2Image" alt="select pokemon">
            <div class="stats">
                HP:
                <progress :value="pokemon2HP" max="255"></progress>
            </div>
            <div class="stats">
                Attack:
                <progress :value="pokemon2Attack" max="190"></progress>
            </div>
            <div class="stats">
                Defence:
                <progress :value="pokemon2Defence" max="250"></progress>
            </div>
            <div class="stats">
                Sp. Attack:
                <progress :value="pokemon2SpAtt" max="194"></progress>
            </div>
            <div class="stats">
                Sp. Defence:
                <progress :value="pokemon2SpDef" max="250"></progress>
            </div>
            <div class="stats">
                Speed:
                <progress :value="pokemon2Speed" max="200"></progress>
            </div>
            <hr/>
            <div class="hp_div">
                <div class="hp_text"> Current HP:</div>
                <progress :value="pokemon2CurrentHP" :max="pokemon2HP" class="main_hp"></progress>
                <div class="hp_text"> {{pokemon2CurrentHP}} / {{pokemon2HP}}</div>
            </div>
            <p>Choose attacking move</p>
            <select @change="updateMove2" v-model="move2" class="pokemon_select">
                <option v-for="move in allMoves" :value="move.name" :key="move">{{move.name}}</option>
            </select>
        </div>
        <button class="battle_button" @click="doBattle">Battle!</button>
    </div>

</template>

<script>
    /* eslint-disable */
    export default {
        created() {
            this.getAllPokemon()
            this.getAllMoves()
        },
        data() {
            return {
                serverHost: "https://viktor-srbinoski-pokemon-api.herokuapp.com",
                pokemon1: null,
                pokemon2: null,
                allPokemon: [],
                pokemon1Image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/Question_Mark.svg/1280px-Question_Mark.svg.png",
                pokemon1HP: 0,
                pokemon1CurrentHP: 0,
                pokemon1Attack: 0,
                pokemon1Defence: 0,
                pokemon1SpAtt: 0,
                pokemon1SpDef: 0,
                pokemon1Speed: 0,

                pokemon2Image: "https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/Question_Mark.svg/1280px-Question_Mark.svg.png",
                pokemon2HP: 0,
                pokemon2CurrentHP: 0,
                pokemon2Attack: 0,
                pokemon2Defence: 0,
                pokemon2SpAtt: 0,
                pokemon2SpDef: 0,
                pokemon2Speed: 0,

                allMoves: [],
                move1: null,
                move2: null,
                move1FullData: null,
                move2FullData: null
            }
        },
        methods: {
            getAllPokemon() {
                console.log("getting all pokemon")
                fetch(this.serverHost + "/pokemon", {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        for (let i = 0; i < data["result"].length; i++) {
                            this.allPokemon.push({name: data["result"][i]["name"], url: data["result"][i]["url"]})
                        }
                    })
            },
            getAllMoves() {
                console.log("getting all moves")
                fetch(this.serverHost + "/moves", {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        for (let i = 0; i < data["result"].length; i++) {
                            this.allMoves.push({name: data["result"][i]["name"], url: data["result"][i]["url"]})
                        }
                    })
            },
            updatePokemon1() {
                fetch(this.serverHost + "/pokemon/" + this.pokemon1, {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        this.pokemon1Image = data["image_url"]
                        this.pokemon1HP = data["base_stats"]["hp"]
                        this.pokemon1CurrentHP = Number(data["base_stats"]["hp"])
                        this.pokemon1Attack = data["base_stats"]["attack"]
                        this.pokemon1Defence = data["base_stats"]["defence"]
                        this.pokemon1SpAtt = data["base_stats"]["sp_attack"]
                        this.pokemon1SpDef = data["base_stats"]["sp_defence"]
                        this.pokemon1Speed = Number(data["base_stats"]["speed"])
                    })
            },
            updatePokemon2() {
                fetch(this.serverHost + "/pokemon/" + this.pokemon2, {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        this.pokemon2Image = data["image_url"]
                        this.pokemon2HP = data["base_stats"]["hp"]
                        this.pokemon2CurrentHP = Number(data["base_stats"]["hp"])
                        this.pokemon2Attack = data["base_stats"]["attack"]
                        this.pokemon2Defence = data["base_stats"]["defence"]
                        this.pokemon2SpAtt = data["base_stats"]["sp_attack"]
                        this.pokemon2SpDef = data["base_stats"]["sp_defence"]
                        this.pokemon2Speed = Number(data["base_stats"]["speed"])
                    })
            },
            doBattle() {
                if (this.pokemon1CurrentHP === 0 || this.pokemon2CurrentHP === 0) {
                    console.log("a pokemon has fainted already")
                    return 0
                }
                if (Number(this.move1FullData.priority) > Number(this.move2FullData.priority)) {
                    console.log("Move 1 has priority")
                    this.attackSequencePokemon1First()

                } else if (Number(this.move2FullData.priority) > Number(this.move1FullData.priority)) {
                    console.log("Move 2 has priority")
                    this.attackSequencePokemon2First()
                } else {
                    console.log("Moves have equal priority, faster pokemon will attack first")
                    if (this.pokemon1Speed >= this.pokemon2Speed) {
                        this.attackSequencePokemon1First()
                    } else {
                        this.attackSequencePokemon2First()
                    }
                }
            },
            attackSequencePokemon1First() {
                fetch(this.serverHost + "/damage/" + this.pokemon2 + "/" + this.pokemon1 + "/" + this.move1, {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        if (Number(data) >= this.pokemon2CurrentHP) {
                            console.log(this.pokemon2 + " fainted")
                            this.pokemon2CurrentHP = 0
                        } else {
                            this.pokemon2CurrentHP -= Number(data)
                            fetch(this.serverHost + "/damage/" + this.pokemon1 + "/" + this.pokemon2 + "/" + this.move2, {
                                method: 'GET',
                                headers: {
                                    'Content-Type': 'application/json'
                                }
                            })
                                .then(response => response.json())
                                .then(data => {
                                    if (Number(data) >= this.pokemon1CurrentHP) {
                                        console.log(this.pokemon1 + " fainted")
                                        this.pokemon1CurrentHP = 0
                                    } else {
                                        this.pokemon1CurrentHP -= Number(data)
                                    }
                                })
                        }
                    })
            },
            attackSequencePokemon2First() {
                fetch(this.serverHost + "/damage/" + this.pokemon1 + "/" + this.pokemon2 + "/" + this.move2, {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        if (Number(data) >= this.pokemon1CurrentHP) {
                            console.log(this.pokemon1 + " fainted")
                            this.pokemon1CurrentHP = 0
                        } else {
                            this.pokemon1CurrentHP -= Number(data)
                            fetch(this.serverHost + "/damage/" + this.pokemon2 + "/" + this.pokemon1 + "/" + this.move1, {
                                method: 'GET',
                                headers: {
                                    'Content-Type': 'application/json'
                                }
                            })
                                .then(response => response.json())
                                .then(data => {
                                    if (Number(data) >= this.pokemon2CurrentHP) {
                                        console.log(this.pokemon2 + " fainted")
                                        this.pokemon2CurrentHP = 0
                                    } else {
                                        this.pokemon2CurrentHP -= Number(data)
                                    }
                                })
                        }
                    })
            },
            updateMove1() {
                fetch(this.serverHost + "/moves/" + this.move1, {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        this.move1FullData = {
                            "name": data["name"],
                            "priority": data["priority"]
                        }
                    })
            },
            updateMove2() {
                fetch(this.serverHost + "/moves/" + this.move2, {
                    method: 'GET',
                    headers: {
                        'Content-Type': 'application/json'
                    }
                })
                    .then(response => response.json())
                    .then(data => {
                        this.move2FullData = {
                            "name": data["name"],
                            "priority": data["priority"]
                        }
                    })
            }
        },
        name: 'PokemonSimulator',
        props: {
            msg: String
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    .image_container {
        padding: 5px;
        width: 48%;
        display: block;
        margin: auto;
        float: left;
    }

    img {
        width: 120px;
        height: 120px;
        display: block;
        margin: auto;
        padding-top: 20px;;
    }

    .pokemon_select {
        display: block;
        margin: auto;
    }

    .central_container {
        margin: auto;
        width: 70%;
    }

    .stats {
        width: 70%;
        text-align: right;
        height: 20px;
        vertical-align: center;
    }

    .main_hp {
        height: 40px;
        width: 50%;
        display: block;
        float: left;
        margin-left: 20px;;
    }

    .hp_div {
        height: 50px;
        width: 100%;

        vertical-align: center;
        display: inline-block;
    }

    .hp_text {
        margin-top: 10px;
        margin-left: 5px;
        display: block;
        float: left;
        width: 15%;
        font-size: small;
    }

    .battle_button {
        height: 50px;
        width: 150px;
        margin-top: 10px;
        font-family: Tahoma;
        font-size: large;
    }
</style>
