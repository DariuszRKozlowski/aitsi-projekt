<template>

<transition name="modal-fade">

    <div class="modal-backdrop">

        <div class="bg-light modal" role="dialog" aria-labelledby="modalTitle" aria-describedby="modalDescription">

            <header class="container-flex p-3 bg-dark text-white modal-header" id="modalTitle">

                <slot name="header">

                    <h1>Informacje o stronie</h1>

                </slot>

            </header>

            <section class="modal-body" id="modalDescription">

                <slot name="body">

                    <div>

                        <p>Na potrzebę zrealizowania projektu z przedmiotu Architektury i Technologie Systemów Internetowych, zdecydowano się na utworzenie aplikacji SPA (Single Page Application)
                            poświęconej grom komputerowym. Aplikacja ta działa bez części serwerowej (jedynie po stronie klienta - przeglądarki WWW). Zaletą takiego podejścia jest między innymi:

                            <ul>

                                <li> Uniknięcie konfigurowania aplikacji po stronie serwera</li>
                                <li> Brak konieczności opłacania hostingu </li>
                                <li> Możliwość otworzenia strony bezpośrednio z pliku </li>
                                <li> Wykorzystanie nowszej technologii - frameworku JavaScriptu</li>
                    
                            </ul>
                            
                        </p>
                        
                        <p>
                            Projekt został wykonany dzięki bibliotece JavaScript – Vue.js, która pozwala na tworzenie prostych webowych aplikacji składających się z komponentów.
                            Wpływ na wybór Vue.js miała jego prostota, gdyż dla osób niezaawansowanych w pracy w technologii JavaScript, Vue.js wydaje się być dobrym startem.
                            W przypadku tego konkretnego frameworka, mamy do czynienia z tzw. niskim progiem wejścia, czyli specjalistyczna wiedza oraz znajomość innych frameworków nie jest od użytkownika wymagana.
                        </p>

                        <p>
                            Kolejnym plusem wybranego rozwiązania jest prostota korzystania z biblioteki, ponieważ aby móc z nią pracować, w kodzie HTML wystarczy dodanie jednego elementu ze znacznikiem &lt;script&gt;.
                            Wszystkim zarządzamy z poziomu kodu JavaScript, a nasze zmiany możemy jednocześnie śledzić w przeglądarce.
                        </p>

                        <p>
                            Innym wartym odnotowania plusem wykorzystania Vue.js jest także jego rozmiar i szybkość działania. 
                            Cały framework zajmuje około 20 kilobajtów, a w porównaniu z działaniem Angulara czy Reacta, Vue.js jest rozwiązaniem szybszym.
                        </p>

                        <p>
                            Dodatkowym atutem Vue.js jest jego bardzo dobra dokumentacja. 
                            W dokumentacji wszystko jest na tyle szczegółowo opisane, że stworzenie aplikacji, nawet dla niedoświadczonej osoby bez obycia z kodem, nie powinno być żadnym problemem.
                        </p>

                        <p>
                            Oprócz wykorzystania Vue.js, do budowy aplikacji wykorzystano również bibliotekę CSS – Bootsrap. 
                            Pozwala on na wizualne budowanie stron internetowych. 
                            Jego niewątpliwą zaletą jest fakt, że znacznie przyspiesza tworzenie użytecznych interfejsów stron i aplikacji internetowych. 
                            Niweluje także różnice intepretowania stylów CSS przez różne przeglądarki, co zwiększa uniwersalność i poprawia kompatybilność. 
                            Podobnie jak w przypadku Vue.js, Bootstrap posiada bardzo dobrą dokumentację, a także wsparcie techniczne na licznych forach dla programistów.
                        </p>

                        <p>
                            Dzięki użyciu Bootstrapa uzyskujemy również efekt responsywności aplikacji. Pozwala to na profesjonalne dostosowywanie treści strony do ekranów różnych rozmiarów.
                            Przez takie podejście uzyskujemy przyjemne dla oka własności wizualne - niezależnie, czy aplikacja wyświetalana jest na ekranie telewizora, laptopa, czy ekranie smartfona.
                        </p>

                    </div>

                </slot>

            </section>

            <footer class="modal-footer">

                <slot name="footer">

                    <div class="btn-toolbar">

                        <button class="deletebutton" @click="zamknij()" aria-label="Zamknij okno">Zamknij okno informacji</button>

                    </div>

                </slot>

            </footer>

        </div>

    </div>

</transition>

</template>

<script>

    export default {

        name: "Informacje",

        data() {
        },

        methods: {

            zamknij() {
                this.$emit("zamknij");
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
