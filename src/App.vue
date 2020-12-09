<template>
    <div id="app">
        <div class="column is-half is-offset-one-quarter">
            <img src="./assets/logo.png" />
            <div class="control">
                <input
                    class="input is-hovered"
                    placeholder="Buscar Pokemon"
                    v-model="search"
                />
            </div>

            <div v-for="(poke, index) in findPokemon" :key="poke.url">
                <Pokemon
                    :name="poke.name"
                    :num="index + 1"
                    :url="poke.url"
                ></Pokemon>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
    name: 'App',
    components: {
        Pokemon
    },
    data() {
        return {
            pokemons: [],
            search: ''
            // filteredPokemons: []
        };
    },
    created: function() {
        axios
            .get('https://pokeapi.co/api/v2/pokemon?limit=100&offset=200')
            .then(res => {
                console.log('pokemons it was saved');
                this.pokemons = res.data.results;
                this.filteredPokemons = res.data.results;
            });
    },
    methods: {
        // searchResult: function() {
        //     this.filteredPokemons = this.pokemons;
        //     if (this.search == '' || this.search == ' ') {
        //         this.filteredPokemons = this.pokemons;
        //     } else {
        //         this.filteredPokemons = this.pokemons.filter(pokemon => {
        //             return (
        //                 this.search.toLowerCase() == pokemon.name.toLowerCase()
        //             );
        //         });
        //     }
        // }
    },
    computed: {
        findPokemon: function() {
            let pokers = this.pokemons.filter(item => {
                let result;
                if (item.name.includes(this.search)) {
                    return (result = item.name);
                }
                console.log(result);
            });
            return pokers;
        }
    }
};
</script>

<style>
#app {
    text-align: center;
}
#search {
    margin-top: 14px;
}
</style>
