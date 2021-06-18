<template>
    <div class="mock">
        <div class="params" v-show="false">
            <label>Nombre de répétion du model : </label>
            <input type="number" />
        </div>

        <div class="mock__editor">
            <textarea id="mockEditor">{ }</textarea>
        </div>

        <button>Obtenir model</button>
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
                required: true
            },
            nbrMock: {
                type: Number,
                required: false,
                default: 0
            }       
        },
        computed: {
            modelToString() {
                return JSON.stringify(this.model, null, "\t");
            }
        },
        methods: {
            genererMock() {
                var modelConcatene = this.modelToString;
                var i = 1;

                while (this.nbrMock > 1 && i < this.nbrMock) {
                    modelConcatene += ", \n" + this.modelToString;
                    i++;
                }

                return modelConcatene;
            }
        },
        mounted() {
            var mockEditor = CodeMirror.fromTextArea(document.getElementById('mockEditor'), { mode: JsMode });
            mockEditor.setSize("425", "400");

            this.mock = mockEditor
        },
        watch: {
            model() {
                this.mock.setValue(this.genererMock());
            },
            nbrMock() {
                this.mock.setValue(this.genererMock());
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
    }
</style>