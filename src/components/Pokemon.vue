<template>
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                <img :src="currentImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{num}} - {{ upper(name)}}</p>
                        <p class="subtitle is-6">{{pokemon.type}}</p>
                    </div>
                </div>

                <div class="content">
                   <button class="button is-fullwidth" @click="mudarSprite">Mudar sprite</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";  

export default {
    created: function () {
        axios.get(this.url).then(resp => {
            this.pokemon.type = resp.data.types[0].type.name;
            this.pokemon.front = resp.data.sprites.front_default;
            this.pokemon.back = resp.data.sprites.back_default;

            this.currentImg = this.pokemon.front;
        });
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String,
    },
    methods: {
        upper: function(value) {
            var newName = value[0].toUpperCase() + value.substring(1);
            return newName ;
        },
        mudarSprite: function() {
            if (this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }
            else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
#pokemon {
    margin-top: 2%;
}
</style>