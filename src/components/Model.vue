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
        
        <button class="mockGenerationButton" id="mockGeneration" @click="genererMock">Générer</button>
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
                model: {}
            };
        },
        mounted() {
            this.model = CodeMirror.fromTextArea(document.getElementById('modelEditor'), { mode: JsMode });
            this.model.setSize("425", "400");
        },
        props: {
            mock: {
                type: Array,
                required: false
            }
        },
        computed: {
            mockToString() {
                return JSON.stringify(this.mock[0], null, "\t");
            },
            modelFormatteJson() {
                return JSON.parse(this.model.getValue().replaceAll("\n", "").replaceAll("\t", ""));
            }
        },
        methods: {
            genererMock() {
                console.log(this.modelFormatteJson);
                this.$emit("genererMock", { nbrMock: this.mockNbrRepetition, model: this.modelFormatteJson });
            },
            genererModel() {
                var modelConcatene = this.mockToString;

                return modelConcatene;
            }
        },
        watch: {
            mock() {
                this.model.setValue(this.genererModel());
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