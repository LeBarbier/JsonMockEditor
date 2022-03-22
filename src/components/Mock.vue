<template>
    <div class="mock">
        <div class="params" >
            <button @click="toggleModal">Ajouter un paramètre</button>
            <button @click="trierParametres">Trier les paramètres</button>
        </div>

        <div class="mock__editor">
            <textarea id="mockEditor">{ }</textarea>
        </div>

        <button class="obtenirModelButton" id="obtenirModel" @click="obtenirModel">Obtenir model</button>
    </div>
</template>

<script>
    import CodeMirror from "../../codemirror/lib/codemirror.js";
    import JsMode from "../../codemirror/mode/javascript/javascript.js";
    import('../../codemirror/lib/codemirror.css');

    export default {
        name: 'Mock',
        data() {
            return {
                mock: {}
            };
        },
        props: {
            model: {
                type: Object,
                required: false
            },
            nbrMock: {
                type: Number,
                required: false,
                default: 0
            },
            nouveauParam: {
                type: Object,
                required: false
            }
        },
        computed: {
            modelToString() {
                return this.convertirJsonEnString(this.model);
            },
            mockFormatteJson() {
                return JSON.parse(this.mock.getValue().replaceAll("\n", "").replaceAll("\t", ""));
            }
        },
        mounted() {
            this.mock = CodeMirror.fromTextArea(document.getElementById('mockEditor'), { mode: JsMode });
            this.mock.setSize("425", "400");
        },
        watch: {
            model() {
                this.mock.setValue(this.genererMock());
            },
            nbrMock() {
                this.mock.setValue(this.genererMock());
            },
            nouveauParam() {
                this.ajouterNouveauParam(this.nouveauParam);
            }
        },
        methods: {
            obtenirModel() {
                console.log(this.mockFormatteJson);
                this.$emit("obtenirModel", { mock: this.mockFormatteJson });
            },
            genererMock() {
                switch (this.nbrMock) {
                    case 0:
                        return "";
                        break;
                    case 1:
                        return "[" + this.modelToString + "]";
                        break;
                    default:
                        return this.concatenerModel();
                        break;
                }
            },
            concatenerModel() {
                var modelConcatene = "[" + this.modelToString;
                var i = 1;

                while (i < this.nbrMock) {
                    modelConcatene += ", \n" + this.modelToString;
                    i++;
                }

                modelConcatene += "]";

                return modelConcatene;
            },
            toggleModal() {
                this.$emit("toggleModal");
            },
            ajouterNouveauParam(param) {
                var mockAvecNouveauParam = [];
                this.mockFormatteJson.forEach(obj => {
                    if (!param.ecraser && !Object.prototype.hasOwnProperty.call(obj, param.nom)) {
                        obj[param.nom] = param.valeur;
                    } else if (param.ecraser) {
                        obj[param.nom] = param.valeur;
                    }
                    mockAvecNouveauParam.push(obj);
                });
                this.mock.setValue(this.convertirJsonEnString(mockAvecNouveauParam));
            },
            trierParametres() {
                var mockParametresTries = [];

                this.mockFormatteJson.forEach(obj => {
                    var objetParamsTries = {};
                    var clefsTries = this.obtenirClefsTries(obj);

                    clefsTries.forEach(clef => {
                        objetParamsTries[clef] = obj[clef];
                    });

                    mockParametresTries.push(objetParamsTries);
                });

                this.mock.setValue(this.convertirJsonEnString(mockParametresTries));
            },
            convertirJsonEnString(model) {
                return JSON.stringify(model, null, "\t");
            },
            obtenirClefsTries(objet) {
                var clefsTries = Object.keys(objet).sort();
                const index = clefsTries.findIndex(element => {
                    return element.toLowerCase() === 'id';
                });

                if (index < 1) {
                    return clefsTries
                }

                const swapTempVar = clefsTries[0];
                clefsTries[0] = clefsTries[index];
                clefsTries[index] = swapTempVar;

                return clefsTries;
            }
        }
    };
</script>

<style scoped>
    .mock {
        padding: 3px;
    }

    .mock__editor {
        margin: 15px 0;
        border: 1px solid black;
    }

    .params {
        border: 1px solid black;
        width: 98%;
        margin-bottom: 4px;
        padding: 2px;
        text-align:center;
    }
</style>