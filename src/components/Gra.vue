<template>
    <div
        v-bind:class="{
            id: gra.id,
            nazwa: gra.nazwa,
            opis: gra.opis,
            cena: gra.cena,
            gatunek: gra.gatunek,
            producent: gra.producent,
            rokWydania: gra.rokWydania,
            fotografiaURL: gra.fotografiaURL
        }"
    >

        <div class = "container-fluid">

            <header class="row text-left"><h1 class="display-4 text-left">{{ gra.id }}. {{ gra.nazwa}}</h1></header>

            <div class="row">

                <div class="col">
                
                    <img class="img-thumbnail rounded float-left" v-bind:src="gra.fotografiaURL"/>

                </div>

                <div class="col-10">

                    <div class="row">

                        <div class="text-left">
                            <p>{{ gra.opis }}</p>
                        </div>

                    </div>

                    <div class="row">

                        <div class="col-2">
                            <b>Cena:</b>
                        </div>

                        <div class="col-3">
                            {{ gra.cena }} PLN
                        </div>

                    </div>

                    <div class="row">

                        <div class="col-2">
                            <b>Producent:</b>
                        </div>

                        <div class="col-3">
                            {{ gra.producent }}
                        </div>

                    </div>

                    <div class="row">

                        <div class="col-2">

                            <b>Rok wydania:</b>

                        </div>

                        <div class="col-3">

                            {{ gra.rokWydania }}

                        </div>

                    </div>

                    <div class="row">

                        <div class="col-2">

                            <b>Gatunek:</b>

                        </div>

                        <div class="col-3">

                            {{ gra.gatunek }}

                        </div>

                    </div>

                    <br/>

                    <div class="row">

                        <div class="btn-toolbar">

                            <button type="button" class="btn btn-sm btn-block editbutton" @click="edytujGre">Edytuj grę</button>
                            <button type="button" class="btn btn-sm btn-block deletebutton" @click="usunGre">Usuń grę</button>

                        </div>

                        <div class="col-2">

                        </div>


                    </div>

                </div>

            </div>

        </div>
    
    </div>

</template>

<script>

    export default {

        props: ["gra"],

        data() {
            return {
            graID: this.gra.id,
            };
        },

        methods: {

            usunGre() {
            this.$emit("graDoUsuniecia", this.graID);
            },

            edytujGre() {
            this.$emit("graDoEdycji", this.graID);
            },

        }

    };

</script>

<style scoped>

    img {
        width: 300px;
        opacity: 0.9;
    }

    .editbutton {
        background-color: deepskyblue;
        margin-right: 5px;
        color: black;
        border: 1px solid black;
    }

    .deletebutton {
        background-color: yellow;
        margin-right: 5px;
        color: black;
        border: 1px solid black;
    }

    .editbutton:hover {
        background-color: greenyellow;
        font-weight: bold;
    }

    .deletebutton:hover {
        background-color: red;
        font-weight: bold;
    }

    img:hover {
        opacity: 1;
    }


</style>
