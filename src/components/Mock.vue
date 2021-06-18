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
                model: {}
            };
        },
        mounted() {
            var mockEditor = CodeMirror.fromTextArea(document.getElementById('mockEditor'), { mode: JsMode, lineNumbers: true });
            mockEditor.setSize("425", "400");

            this.model = mockEditor
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