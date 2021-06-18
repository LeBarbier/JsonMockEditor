<template>
    <div class="model">
        <div class="params">
            <div>
                <label for="mockNbrRepetition">Nombre de répétion du model : </label>
                <input v-model.number="mockNbrRepetition" id="mockNbrRepetition" type="number" />
            </div>
        </div>

        <div class="model__editor">
            <textarea id="modelEditor">{ }</textarea>
        </div>
        
        <button class="mockGenerationButton" id="mockGeneration" @click="generateMock">Générer</button>
    </div>
</template>

<script>
    import CodeMirror from "../../codemirror/lib/codemirror.js";
    import JsMode from "../../codemirror/mode/javascript/javascript.js";
    import('../../codemirror/lib/codemirror.css');
    
    export default {
        name: 'Model',
        data() {
            return {
                mockNbrRepetition: 1,
                modelEditor: {},
                model: ""
            };
        },
        mounted() {
            this.modelEditor = CodeMirror.fromTextArea(document.getElementById('modelEditor'), { mode: JsMode });
            this.modelEditor.setSize("425", "400");

            this.model = this.obtenirModelEditor;
        },
        computed: {
            obtenirModelEditor() {
                return JSON.parse(this.modelEditor.getValue().replaceAll("\n", "").replaceAll("\t", ""));
            }
        },
        methods: {
            generateMock() {
                console.log(this.obtenirModelEditor);
                this.$emit("genererMock", { nbrMock: this.mockNbrRepetition, model: this.obtenirModelEditor });
            }
        }
    };
</script>

<style scoped>
    .model {
        padding: 3px;
    }

    .model__editor {
        margin: 15px 0;
        border: 1px solid black;
    }

    .params {
        border: 1px solid black;
        width: 98%;
        margin-bottom: 4px;
        padding: 2px;
    }
</style>