<template>

<transition name="modal-fade">

    <div class="modal-backdrop">

        <div class="bg-light modal" role="dialog" aria-labelledby="modalTitle" aria-describedby="modalDescription">

            <header class="container-flex p-3 bg-dark text-white modal-header" id="modalTitle">

                <slot name="header">

                    <h1>Dodaj nową grę</h1>

                </slot>

            </header>

            <section class="modal-body" id="modalDescription">

                <slot name="body">

                    <div>

                        <div>

                            <label><b>Nazwa gry: </b><br/><input id="nazwa_gry" type="text" v-model="nazwaNowejGry"/></label>

                        </div>

                        <div>

                            <label><b>Cena gry: </b><br/><input id="cena_gry" type="number" min="99.99" step="0.1" v-model="cenaNowejGry"/></label>

                        </div>

                        <div>

                            <label><b>Opis gry: </b><br/><textarea id="opis_gry" type="text" v-model="opisNowejGry"/></label>

                        </div>

                        <div>

                            <label><b>Link do zdjęcia gry: </b><br/><input id="link_do_zdjecia" type="text" v-model="fotografiaNowejGry"/></label>

                        </div>

                        <div>

                            <label><b>Producent gry: </b><br/><input id="producent_gry" type="text" v-model="producentNowejGry" /></label>

                        </div>

                        <div>

                            <label><b>Gatunek gry: </b><br/><input id="gatunek_gry" type="text" v-model="gatunekNowejGry"/></label>

                        </div>

                        <div>

                            <label><b>Rok wydania gry: </b><br/><input id="rok_wydania_gry" type="number" min="1990" max="2021" step="1" v-model="rokWydaniaNowejGry"/></label>

                        </div>

                    </div>

                </slot>

            </section>

            <footer class="modal-footer">

                <slot name="footer">

                    <div class="btn-toolbar">

                        <button class="editbutton" @click="dodajNowaGre()">Dodaj grę</button>

                        <button class="deletebutton" @click="zamknij()" aria-label="Zamknij okno">Zamknij okno</button>

                    </div>

                </slot>

            </footer>

        </div>

    </div>

</transition>

</template>

<script>

    export default {

        name: "DodajGre",

        data() {

            return {
            nazwaNowejGry: "Nazwa nowej gry",
            opisNowejGry: "Opis nowej gry",
            cenaNowejGry: 99.99,
            gatunekNowejGry: "Gatunek nowej gry",
            producentNowejGry: "Producent nowej gry",
            rokWydaniaNowejGry: 2021,
            fotografiaNowejGry: "https://www.adr-shop.com/media/77/catalog/cd-rohlinge-ritek-bedruckbar-bis-25mm-thermo-silber.jpg"
            };
        },

        methods: {

            zamknij() {
                this.$emit("zamknij");
            },

            dodajNowaGre() {
                
                this.$emit(
                    "dodajNowaGre",
                    this.nazwaNowejGry,
                    this.opisNowejGry,
                    this.cenaNowejGry,
                    this.gatunekNowejGry,
                    this.producentNowejGry,
                    this.rokWydaniaNowejGry,
                    this.fotografiaNowejGry
                );
            },
        },
    };

</script>

<style scoped>

    .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    position: relative;
    border-bottom: 1px solid #eeeeee;
    color: #4AAE9B;
    justify-content: space-between;
  }

  .modal-footer {
    border-top: 1px solid #eeeeee;
    flex-direction: column;
    justify-content: flex-end;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    padding: 10px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #4AAE9B;
    border: 1px solid #4AAE9B;
    border-radius: 2px;
  }

    .modal-fade-enter,
  .modal-fade-leave-to {
    opacity: 0;
  }

    .modal-fade-enter-active,
  .modal-fade-leave-active {
    transition: opacity .5s ease;
  }

  textarea {
      width: 190px;
      height: 190px;
      resize: none;
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

</style>
