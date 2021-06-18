<template>
    <div class="infos">
        <h3>Commandes :</h3>
        <table>
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
        margin-top: 10px;
        width: 100%;
    }

    td, th {
        border: 1px solid grey;
        padding: 2px 8px;
    }
</style>