<template>
    <div id="pokemon">
        <div class="card">
            <h1 v-show="msg">mensagem aqui</h1>
            <div class="card-image">
                <figure>
                        <img :src="currentImg" alt="Placeholder image" />
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                        <div class="media-content">
                            <p class="title is-4">
                                {{ num }}. {{ upper(nome) }}
                            </p>
                            <p class="subtitle is-6">
                                {{ pokemon.typePoke }}
                            </p>
                            <hr />
                            <button
                                ref="bttChange"
                                class="button is-info is-dark"
                                @click="changeSprit">
                                Change to back view
                            </button>
                        </div>
                </div>

                <div class="content"></div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    created() {
        axios.get(this.url).then((res) => {
            //Criando var type pra receber tipo de pokemon:
            
            this.pokemon.typePoke = res.data.types[0].type.name;
            //Pegando imagem de pokemon, frente/costas:
            this.pokemon.frontPoke = res.data.sprites.front_default;
            this.pokemon.backPoke = res.data.sprites.back_default;
            this.currentImg = this.pokemon.frontPoke;
            console.log(this.pokemon);
        });
    },

    data() {
        return {
            msg: false,
            isFront: true,
            currentImg: "",

            pokemon: {
                typePoke: "", // Inicializando com uma propriedade vazia
                frontPoke: "", // Inicializando com uma propriedade vazia
                backPoke: "",
            },
        };
    },

    props: {
        num: Number,
        nome: String,
        url: String,
    },

    methods: {
        //transforma 1 letra de string em maiúscula:
        upper(value) {
            if (!value) {
                return "";
            } else {
                return value[0].toUpperCase() + value.slice(1);
            }
        },

        changeSprit() {
            if (this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.backPoke;
                this.$refs.bttChange.classList.add(
                        "button",
                        "is-danger",
                        "is-dark"
                );
                this.$refs.bttChange.innerText = "Return to front view";
            } else {
                this.isFront = true;
                this.currentImg = this.pokemon.frontPoke;
                this.$refs.bttChange.classList.remove(
                        "button",
                        "is-danger",
                        "is-dark"
                );
                this.$refs.bttChange.classList.add(
                        "button",
                        "is-info",
                        "is-dark"
                );
                this.$refs.bttChange.innerText = "Change to back view";
            }
        },
    },
};
</script>

<style>
img {
     height: 30%;
     width: 30%;
}
#pokemon {
     margin: 40px 0px 40px 0px;
}
</style>
