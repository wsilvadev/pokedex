<template>
    <div class="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="currentImg" alt="Placeholder image" />
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{ name | upper }}</p>
                        <p class="subtitle is-6">{{ pokemon.type }}</p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-fullwidth" v-on:click="reverser">
                        Inverter pokemon
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    created: function() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        });
    },
    data() {
        return {
            isSprites: true,
            currentImg: '',
            pokemon: { type: '', front: '', back: '' }
        };
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(text) {
            const newText = text.charAt(0).toUpperCase() + text.slice(1);
            return newText;
        }
    },
    methods: {
        reverser: function() {
            if (this.isSprites) {
                this.isSprites = false;
                this.currentImg = this.pokemon.back;
            } else {
                this.isSprites = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
};
</script>

<style scoped>
.pokemon {
    margin: 15px;
}
</style>
