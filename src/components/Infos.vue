<template>
    <div class="infos">
        <h4>
            Créer un model JSON et "Générer" pour pouvoir obtenir une liste de ce model.
            <br />
            Ajouter une liste d'objet JSON et "Obtenir model" pour obtenir le model du premier objet de la liste.
            <br />
            "Ajouter un paramètre" permet d'ajouter un paramètre avec une valeur par défaut à tout les objets de la liste.
        </h4>

        <h3 v-show="false">Commandes :</h3>
        <table v-show="false">
            <thead>
                <tr>
                    <th>Commande</th>
                    <th>Paramètres</th>
                    <th>Description</th>
                </tr>
            </thead>
            <tr>
                <td>Integer(0 à 9999)</td>
                <td>Intervalle désiré</td>
                <td>Génère un nombre entier aléatoire</td>
            </tr>
            <tr>
                <td>Float(0 à 9999, 0 à 9)</td>
                <td>Intervalle désiré et nombre de chiffre après la virgule</td>
            </tr>
            <tr>
                <td>Lorem(0 à 9999)</td>
                <td>Nombre de charactère</td>
                <td>Génère du texte lorem ipsum.</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {

    }
</script>

<style scoped>
    .infos {
        margin-top: 16px;
        width: 100%;
        text-align: center;
    }

    h4 {
        line-height: 22px;
        font-weight: 400;
    }

    td, th {
        border: 1px solid grey;
        padding: 2px 8px;
    }
</style>