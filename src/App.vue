<template>
  <div class="bg-light">
    <div class="container-flex p-3 bg-dark text-white">

      <h1 class="display-1 text-center">Katalog zainstalowanych gier komputerowych</h1>

    </div>


    <nav class="container-flex p-3">

      <div>

        <span>

          <div>
            <button type="button" class="btn btn-primary btn-sm button"  @click="wyswietlOknoDodawania()">Dodaj nową grę</button>
            <button type="button" class="btn btn-primary btn-sm button"  @click="wyswietlOknoInformacji()">Informacje o stronie</button>
          </div>

          <br/>

        </span>

        <div class="container">

          <div class="row">

            <div class="col">

              <div>

                <div>

                  <br/>
                  <p class="text-dark"><b>Dostosuj na podstawie ceny:</b></p>

                  <input
                    name="cenaMinimalna"
                    type="number"
                    min="1"
                    step="1"
                    placeholder="Od (zł)"
                    v-model="cenaMinimalna"
                  />
                </div>

                <div>

                  <input
                    name="cenaMaksymalna"
                    type="number"
                    min="2"
                    step="1"
                    placeholder="Do (zł)"
                    v-model="cenaMaksymalna"
                  />

                </div>

                <br/>

              </div>

              <div class="row-sm-5">

                <div class="col">

                  <button class="btn btn-primary btn-sm btn-block filterbutton" @click="filtrujPoPrzedzialeCen">Filtruj</button>

                </div>

                <div class="col-sm-5">

                  <button class="btn btn-primary btn-sm btn-block filterbutton" @click="resetujFiltrowanie">Resetuj filtrowanie</button>

                </div>

              </div>

            </div>

            <div class="col">

              <div>

                  <br/>
                  <p class="text-dark"><b>Sortuj przy użyciu:</b></p>

              </div>

              <div class="container">

                <div class="btn-toolbar">

                  <button type="button" class="btn btn-primary btn-sm filterbutton" @click="sortujPoID('R')">ID (rosnąco)</button>

                  <button type="button" class="btn btn-primary btn-sm filterbutton" @click="sortujPoID('M')">ID (malejąco)</button>

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoNazwie('R')">Nazwa (rosnąco)</button>

                </div>

                <div class="btn-toolbar">

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoNazwie('M')">Nazwa (malejąco)</button>

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoCenie('R')">Cena (rosnąco)</button>

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoCenie('M')">Cena (malejąco)</button>

                </div>


                <div class="btn-toolbar">

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoDacie('R')">Rok (rosnąco)</button>

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoDacie('M')">Rok (malejąco)</button> 

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoGatunku('R')">Gatunek (rosnąco)</button>

                </div>


                <div class="btn-toolbar">

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoGatunku('M')">Gatunek (malejąco)</button>

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoProducencie('R')">Producent (rosnąco)</button>

                  <button type="button" class="btn btn-primary btn-sm btn-block filterbutton" @click="sortujPoProducencie('M')">Producent (malejąco)</button>

                </div>

              </div>

            </div>

          
          </div>

        </div>

      </div>

    </nav>

    <div class="divgry">

      <Gra

        class="gra"
        v-bind:gra="gra"
        v-for="gra in gry"
        :key="gra.id"

        @graDoEdycji="wyswietlOknoEdycji"
        @graDoUsuniecia="usunGre"

      />

    </div>

  </div>

    <DodajGre

      v-show="widocznoscOknaDodawania"
      @zamknij="zamknijOknoDodawania()"
      @dodajNowaGre="dodajGre"
    />

    <EdytujGre

      v-show="widocznoscOknaEdycji"
      @zamknij="zamknijOknoEdycji()"
      @edytujIstniejacaGre="edytujGre"

    />

    <Informacje

      v-show="widocznoscOknaInformacji"
      @zamknij="zamknijOknoInformacji()"

    />

</template>

<script>

  import Gra from "./components/Gra.vue";
  import DodajGre from "./components/DodajGre.vue";
  import EdytujGre from "./components/EdytujGre.vue";
  import Informacje from "./components/Informacje.vue";

  export default {

    name: "App",

    components: {
      Gra,
      DodajGre,
      EdytujGre,
      Informacje
    },

    data() {
      return {
        gry: [
          { 
            id: 1,
            nazwa: "Wiedźmin 3: Dziki Gon",
            opis: "Gra jest kontynuacją wydanego w 2007 roku Wiedźmina oraz Wiedźmina 2: Zabójców królów. Tak jak poprzednie części, opowiada ona historię tytułowego wiedźmina – Geralta z Rivii.",
            cena: 119.99,
            gatunek: "Akcja",
            producent: "CD Projekt Red",
            rokWydania: 2015,
            fotografiaURL: "https://cdn.gracza.pl/galeria/gry13/grupy/544003500.jpg"
          },

          { 
            id: 2,
            nazwa: "FIFA 22",
            opis: "Symulacyjna gra wideo stowarzyszenia piłkarskiego wydana przez Electronic Arts w ramach serii FIFA. Jest to 29. odsłona serii FIFA. W grze występuje ponad 30 oficjalnych lig, ponad 700 klubów piłkarskich i ponad 17 000 piłkarzy.",
            cena: 149.99,
            gatunek: "Sportowe",
            producent: "EA Sports",
            rokWydania: 2021,
            fotografiaURL: "https://upload.wikimedia.org/wikipedia/en/6/6c/FIFA_22_Cover.jpg"
          },

          {
            id: 3,
            nazwa: "Counter-Strike: Global Offensive",
            opis: "Wieloosobowa strzelanka pierwszoosobowa, stworzona oraz wydana przez Valve Corporation i Hidden Path Entertainment, które już wcześciej pracowały nad Counter-Strike: Source. Zadaniem każdej z drużyn jest eliminacja drużyny przeciwnej lub wykonanie określonego zadania.",
            cena: 139.99,
            gatunek: "Strzelanka",
            producent: "Valve Corporation",
            rokWydania: 2012,
            fotografiaURL: "https://image.ceneostatic.pl/data/products/78971434/i-cs-go-prime-status-upgrade-digital.jpg"
          },

          {
            id: 4,
            nazwa: "Grand Theft Auto V",
            opis: "Gra skupia się na przestępczości w jednej z metropolii Stanów Zjednoczonych – Los Santos i jej obrębie w stanie San Andreas. Trzej protagoniści (nad którymi gracz ma kontrolę), mimo że zajmują się innymi rodzajami przestępstw jako tzw. „wolni strzelcy”, współpracują ze sobą oraz wspólnie zajmują się nielegalnymi interesami",
            cena: 139.99,
            gatunek: "Akcja",
            producent: "Rockstar North",
            rokWydania: 2015,
            fotografiaURL: "https://cdn-products.eneba.com/resized-products/s29Db6ZBVLneuD0t66qnYRamvGDP3p8chLz-3IomxcU_350x200_3x-0.jpeg"
          },

          {
            id: 5,
            nazwa: "F1 2021",
            opis: "Oficjalna gra wideo mistrzostw Formuły 1 oraz Formuły 2, opracowana przez Codemasters i opublikowana przez EA Sports.",
            cena: 269.99,
            gatunek: "Sportowe",
            producent: "EA Sports",
            rokWydania: 2021,
            fotografiaURL: "https://upload.wikimedia.org/wikipedia/en/8/86/F1_2021_cover_art.jpg"
          }
        ],

        indeksPoczatkowy: 6,
        widocznoscOknaDodawania: false,
        widocznoscOknaEdycji: false,
        widocznoscOknaInformacji: false,
        typSortowania: "R",
        domyslneIdDoEdycji: 0,
        cenaMinimalna: null,
        cenaMaksymalna: null,
        gryDoFiltrowania: null,


      };
    },

    methods: {

      dodajGre(nazwaNowejGry, opisNowejGry, cenaNowejGry, gatunekNowejGry, producentNowejGry, rokWydaniaNowejGry, fotografiaNowejGry) {

        this.gry.push({
          id: this.indeksPoczatkowy++,
          nazwa: nazwaNowejGry,
          opis: opisNowejGry,
          cena: cenaNowejGry,
          gatunek: gatunekNowejGry,
          producent: producentNowejGry,
          rokWydania: rokWydaniaNowejGry,
          fotografiaURL: fotografiaNowejGry
        });

        this.widocznoscOknaDodawania = false;
      },

      edytujGre(nazwaEdytowanejGry, opisEdytowanejGry, cenaEdytowanejGry, gatunekEdytowanejGry, producentEdytowanejGry, rokWydaniaEdytowanejGry, fotografiaEdytowanejGry) {

        const indeksDoEdycji = this.gry.findIndex((gra) => gra.id === this.domyslneIdDoEdycji);

        this.gry[indeksDoEdycji].nazwa = nazwaEdytowanejGry;
        this.gry[indeksDoEdycji].opis = opisEdytowanejGry;
        this.gry[indeksDoEdycji].cena = cenaEdytowanejGry;
        this.gry[indeksDoEdycji].gatunek = gatunekEdytowanejGry;
        this.gry[indeksDoEdycji].producent = producentEdytowanejGry;
        this.gry[indeksDoEdycji].rokWydania = rokWydaniaEdytowanejGry;
        this.gry[indeksDoEdycji].fotografiaURL = fotografiaEdytowanejGry;

        this.widocznoscOknaEdycji = false;
      },

      usunGre(idGryDoUsuniecia) {
        
        const indeksDoUsuniecia = this.gry.findIndex((gra) => gra.id === idGryDoUsuniecia);
        this.gry.splice(indeksDoUsuniecia, 1);

      },

      wyswietlOknoEdycji(idGryDoEdycji) {
        this.domyslneIdDoEdycji = idGryDoEdycji;
        this.widocznoscOknaEdycji = true;
      },

      wyswietlOknoDodawania() {
        this.widocznoscOknaDodawania = true;
      },

      wyswietlOknoInformacji() {
        this.widocznoscOknaInformacji = true;
      },

      zamknijOknoEdycji() {
        this.widocznoscOknaEdycji = false;
      },

      zamknijOknoDodawania() {
        this.widocznoscOknaDodawania = false;
      },

      zamknijOknoInformacji() {
        this.widocznoscOknaInformacji = false;
      },

      filtrujPoPrzedzialeCen() {

        this.gryDoFiltrowania = this.gry;

        if(this.cenaMinimalna && this.cenaMaksymalna) {
          this.gry = this.gry.filter((gra) => gra.cena <= this.cenaMaksymalna && gra.cena >= this.cenaMinimalna).sort((graA, graB) => graA.cena - graB.cena);
        }
        else if(this.cenaMinimalna && !this.cenaMaksymalna) {
          this.gry = this.gry.filter((gra) => gra.cena >= this.cenaMinimalna).sort((graA, graB) => graA.cena - graB.cena);
        }
        else if(!this.cenaMinimalna && this.cenaMaksymalna) {
          this.gry = this.gry.filter((gra) => gra.cena <= this.cenaMaksymalna).sort((graA, graB) => graA.cena - graB.cena);
        }  
      },

      resetujFiltrowanie() {

        if(this.gryDoFiltrowania != null) {
          this.gry = this.gryDoFiltrowania.sort((graA, graB) => graA.id - graB.id);
          this.cenaMinimalna = null;
          this.cenaMaksymalna = null;
        } 
      },

      sortujPoID(znak) {

        this.typSortowania = znak;

        switch(this.typSortowania) {

          case "R":
            return this.gry.sort(function (graA, graB) {
              var idGryA = graA.id;
              var idGryB = graB.id;

              return (idGryA < idGryB ? -1 : (idGryA > idGryB ? 1 : 0));

            });

          case "M":
              return this.gry.sort(function (graA, graB) {
              var idGryA = graA.id;
              var idGryB = graB.id;

              return (idGryA > idGryB ? -1 : (idGryA < idGryB ? 1 : 0));

            });

        }

      },

      sortujPoNazwie(znak) {

        this.typSortowania = znak;

        switch(this.typSortowania) {

          case "R":
            return this.gry.sort(function (graA, graB) {
              var nazwaGryA = graA.nazwa.toLowerCase();
              var nazwaGryB = graB.nazwa.toLowerCase();

              return (nazwaGryA < nazwaGryB ? -1 : (nazwaGryA > nazwaGryB ? 1 : 0));

            });

          case "M":
            return this.gry.sort(function (graA, graB) {
              var nazwaGryA = graA.nazwa.toLowerCase();
              var nazwaGryB = graB.nazwa.toLowerCase();

              return (nazwaGryA > nazwaGryB ? -1 : (nazwaGryA < nazwaGryB ? 1 : 0));

            });

        }
      },

      sortujPoCenie(znak) {

        this.typSortowania = znak;

        switch(this.typSortowania) {

          case "R":
            return this.gry.sort(function (graA, graB) {
              var cenaGryA = graA.cena;
              var cenaGryB = graB.cena;

              if(cenaGryA == cenaGryB) {
                return 0;
              }
              else {
                return cenaGryA < cenaGryB ? -1 : 1;
              }
            });

          case "M":
            return this.gry.sort(function (graA, graB) {
              var cenaGryA = graA.cena;
              var cenaGryB = graB.cena;

              if(cenaGryA == cenaGryB) {
                return 0;
              }
              else {
                return cenaGryA > cenaGryB ? -1 : 1;
              }
            });
        }

      },

      sortujPoDacie(znak) {

        this.typSortowania = znak;

        switch(this.typSortowania) {

          case "R":
            return this.gry.sort(function (graA, graB) {
              var dataGryA = graA.rokWydania;
              var dataGryB = graB.rokWydania;

              if(dataGryA == dataGryB) {
                return 0;
              }
              else {
                return dataGryA < dataGryB ? -1 : 1;
              }
            });

          case "M":
            return this.gry.sort(function (graA, graB) {
              var dataGryA = graA.rokWydania;
              var dataGryB = graB.rokWydania;

              if(dataGryA == dataGryB) {
                return 0;
              }
              else {
                return dataGryA > dataGryB ? -1 : 1;
              }
            });
        }
      },

      sortujPoGatunku(znak) {

        this.typSortowania = znak;

        switch(this.typSortowania) {

          case "R":
            return this.gry.sort(function (graA, graB) {
              var gatunekGryA = graA.gatunek.toLowerCase();
              var gatunekGryB = graB.gatunek.toLowerCase();

              return (gatunekGryA < gatunekGryB ? -1 : (gatunekGryA > gatunekGryB ? 1 : 0));


            });

          case "M":
            return this.gry.sort(function (graA, graB) {
              var gatunekGryA = graA.gatunek.toLowerCase();
              var gatunekGryB = graB.gatunek.toLowerCase();

              return (gatunekGryA > gatunekGryB ? -1 : (gatunekGryA < gatunekGryB ? 1 : 0));

            });

        }

      },

      sortujPoProducencie(znak) {

        this.typSortowania = znak;

        switch(this.typSortowania) {

          case "R":
            return this.gry.sort(function (graA, graB) {
              var producentGryA = graA.producent.toLowerCase();
              var producentGryB = graB.producent.toLowerCase();

              return (producentGryA < producentGryB ? -1 : (producentGryA > producentGryB ? 1 : 0));

            });

          case "M":
            return this.gry.sort(function (graA, graB) {
              var producentGryA = graA.producent.toLowerCase();
              var producentGryB = graB.producent.toLowerCase();

              return (producentGryA > producentGryB ? -1 : (producentGryA < producentGryB ? 1 : 0));
            });

        }
      } 

    }
  }
</script>

<style scoped>

  .button {
    width: 100%;
    height: 50px;
    display: block;
    background-color: #ADFF2F;
    color: black;
    font-size: 25px;
  }

  .filterbutton {
    margin-bottom: 5px;
    margin-right: 5px;
    background-color: #ADFF2F;
    color: black;
  }

  .filterbutton:hover, .button:hover {
    font-weight: bold;
  }

  .gra {
    padding: 10px;
    margin-bottom: 5px;
    border: 1px solid black;
  }

  .divgry {
    width:75%;
    margin-left:auto;
    margin-right:auto;
    background-color: bisque;
  }

</style>


