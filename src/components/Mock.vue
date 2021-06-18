<template>
    <div class="mock">
        <textarea v-model="mock"></textarea>
    </div>
</template>

<script>
    export default {
        name: 'Mock',
        props: {
            mock: {
                type: String,
                required: false,
                default: null
            }
        },
        mounted() {
            this.addKeyDownEventListener();
        },
        methods: {
            addKeyDownEventListener() {
                document.getElementById('modelTextArea').addEventListener('keydown', function (e) {
                    if (e.key == 'Tab') {
                        e.preventDefault();
                        var start = this.selectionStart;
                        var end = this.selectionEnd;

                        // set textarea value to: text before caret + tab + text after caret
                        this.value = this.value.substring(0, start) +
                            "\t" + this.value.substring(end);

                        // put caret at right position again
                        this.selectionStart =
                            this.selectionEnd = start + 1;
                    }
                });
            }
        }
    };
</script>

<style scoped>
    .mock {
        height: 500px;
        width: 98%;
        padding: 3px;
        border: 1px solid black;
    }

    .mock textarea {
        width: 98%;
        height: 98%;
        margin: 0 auto;
        padding: 2px;
        resize: none;
        font-size: 16px;
        font-family: monospace;
    }
</style>

<!--
function prettyPrint() {
    var ugly = document.getElementById('myTextArea').value;
    var obj = JSON.parse(ugly);
    var pretty = JSON.stringify(obj, undefined, 4);
    document.getElementById('myTextArea').value = pretty;
}    
-->