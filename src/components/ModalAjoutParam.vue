﻿<template>
    <div class="modalAjoutParam">
        <div class="infosParam">
            <div>
                <label for="nomParam">Nom du paramètre :</label>
                <input id="nomParam" type="text" v-model="nom" />
            </div>

            <br />

            <div>
                <label for="valeurDefautParam">Valeur par défaut :</label>
                <input id="valeurDefautParam" type="text" v-model="valeur" />
            </div>

            <br />

            <div>
                <label for="ecraserValeurExistante">Écraser la valeur existante : </label>
                <input id="ecraserValeurExistante" type="checkbox" v-model="ecraser" />
            </div>
        </div>

        <button @click="fermer">Annuler</button>
        <button @click="ajouter">Ajouter</button>
    </div>
</template>

<script>
    export default {
        name: 'ModalAjoutParam',
        data() {
            return {
                nom: '',
                valeur: '',
                ecraser: false
            }
        },
        methods: {
            fermer() {
                this.$emit('toggleModal', null);
            },
            ajouter() {
                this.$emit('toggleModal', { nom: this.nom, valeur: this.valeur, ecraser: this.ecraser });
            }
        }
    }
</script>

<style scoped>
    .modalAjoutParam {
        z-index: 1000;
        position: absolute;
        background-color: white;
        border: 1px solid black;
        width: 425px;
        top: 125px;
        left: calc(48% - 200px);
    }

    .infosParam {
        width: 95%;
        display: inline-block;
        padding: 12px 2px;
    }

    .infosParam label {
        margin-left: 12px;
    }

    .infosParam input {
        margin: 0px 12px;
        float: right;
    }

    button {
        float: right;
        vertical-align: bottom;
        margin: 4px 32px;
    }
</style>