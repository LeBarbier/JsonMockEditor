﻿<template>
    <div class="home">
        <div :class="{ greyedOut: afficherModalAjoutParam }">
            <div class="gestionModel">
                <model :mock="mock"
                       @genererMock="(value) => genererMock(value)"/>
            </div>

            <div class="gestionMock">
                <mock :nbr-mock="nbrMock"
                      :model="model"
                      :nouveau-param="nouveauParam"
                      @obtenirModel="(value) => obtenirModel(value)"
                      @toggleModal="() => afficherModalAjoutParam = !afficherModalAjoutParam" />
            </div>
        </div>

        <modal-ajout-param v-if="afficherModalAjoutParam"
                           @toggleModal="(value) => fermerModal(value)" />
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
                model: {},
                mock: [],
                nbrMock: 1,
                nouveauParam: {},
                afficherModalAjoutParam: false
            };
        },
        components: {
            'model': Model,
            'mock': Mock,
            'modal-ajout-param': ModalAjoutParam,
            'infos': Infos
        },
        methods: {
            genererMock(value) {
                this.model = value.model;
                this.nbrMock = value.nbrMock;
            },
            obtenirModel(value) {
                this.mock = value.mock;
            },
            fermerModal(param) {
                if (param !== null && param.nom !== '' && param.valeur !== '') {
                    this.nouveauParam = param;
                }

                this.afficherModalAjoutParam = !this.afficherModalAjoutParam;
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

    .gestionModel, .gestionMock {
        margin: 12px;
        display: inline-block;
    }

    .greyedOut {
        opacity: 0.5;
    }
</style>