<template>
    <div class="home">
        <div :class="{ greyedOut: afficherModalAjoutParam }">
            <div class="jsonObject">
                <div class="params">
                    <div>
                        <label for="mockNbrRepetition">Nombre de répétion du model : </label>
                        <input v-model.number="mockNbrRepetition" id="mockNbrRepetition" type="number" />
                    </div>
                </div>

                <div v-if="jsonUnparsable" class="jsonError">Erreur lors du JSON.parse</div>
                <model @model="(value) => model = value"
                       @jsonUnparsable="(value) => jsonUnparsable = value" />
            </div>

            <button class="mockGenerationButton" id="mockGeneration" @click="generateMock">Générer</button>

            <div class="gestionMock">
                <!-- À faire -->
                <div class="params" v-show="false">
                    <label for="ajoutParam">Ajouter un paramètre au mock</label>
                    <button id="ajoutParam" @click="() => afficherModalAjoutParam = !afficherModalAjoutParam">>></button>
                </div>
                <mock :mock="mock" />
            </div>
        </div>

        <modal-ajout-param v-if="afficherModalAjoutParam" @fermerModal="fermerModal" />
        <infos />
    </div>
</template>

<script>
    import Model from './Model.vue';
    import Mock from './Mock.vue';
    import ModalAjoutParam from './ModalAjoutParam.vue';
    import Infos from './Infos.vue';

    export default {
        name: 'Home',
        data() {
            return {
                jsonUnparsable: false,
                mockNbrRepetition: 1,
                model: {},
                mock: '',
                afficherModalAjoutParam: false
            };
        },
        components: {
            'model': Model,
            'mock': Mock,
            'modal-ajout-param': ModalAjoutParam,
            'infos': Infos
        },
        computed: {
            showJsonError() {
                return this.jsonUnparsable;
            }
        },
        methods: {
            fermerModal(param) {
                if (param !== null) {

                }

                this.afficherModalAjoutParam = !this.afficherModalAjoutParam;
            },
            generateMock() {
                if (this.mockNbrRepetition > 0) {
                    this.mock = this.model;
                    for (var i = 1; i < this.mockNbrRepetition; i++) {
                        this.mock += ', \n' + this.model;
                    }
                }
            }
        }
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .home {
        width: 100%;
        height: 100%;
    }

    .home div {
        display: inline-block;
    }

    .jsonObject {
        height: 100%;
        width: calc(47% - 30px);
        margin: 12px;
    }

    .gestionMock {
        height: 100%;
        width: calc(47% - 30px);
        margin: 12px;
    }

    .gestionMock div {
        padding: 4px;
    }

    .gestionMock button {
        margin: 0px 10px;
    }

    .params {
        border: 1px solid black;
        width: 98%;
        margin-bottom: 4px;
        padding: 2px;
    }

    .params div{
        padding: 4px;
    }

    .params button {
        margin: 0px 10px;
    }

    .greyedOut {
        opacity: 0.5;
    }

    .mockGenerationButton {
    }
</style>

<!-- style pour la liste de model à gauche
    right: 0px;
    position: absolute;
    border: 2px solid black;
    width: 45%;
    height: 98%;
    padding: 3px;
-->
