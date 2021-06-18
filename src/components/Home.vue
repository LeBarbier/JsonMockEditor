<template>
    <div class="home">
        <div :class="{ greyedOut: afficherModalAjoutParam }">
            <div class="gestionModel">
                <!--<div v-if="jsonUnparsable" class="jsonError">Erreur lors du JSON.parse</div>-->
                <model @genererMock="(value) => genererMock(value)"/>
            </div>

            <div class="gestionMock">
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
        //computed: {
        //    showJsonError() {
        //        return this.jsonUnparsable;
        //    }
        //},
        methods: {
            genererMock(value) {
                this.model = value;
            },
            fermerModal(param) {
                if (param !== null) {

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