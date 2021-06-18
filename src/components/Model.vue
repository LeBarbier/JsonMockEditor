<template>
    <div class="model">
        <textarea id="modelTextArea" v-model="model"></textarea>
    </div>
</template>

<script>
    export default {
        name: 'Model',
        data() {
            return {
                model: '',
                modelJSON: null
            };
        },
        mounted() {
            this.addKeyDownEventListener();
        },
        watch: {
            model: function () {
                try {
                    this.modelJSON = JSON.parse(this.model);
                    this.model = JSON.stringify(this.modelJSON, null, '\t');

                    this.$emit('jsonUnparsable', false);
                    this.$emit('model', this.model);
                } catch {
                    this.$emit('jsonUnparsable', true);
                }
            }
        },
        methods: {
            addKeyDownEventListener() {
                document.getElementById('modelTextArea').addEventListener('keydown', function (e) {
                    if (e.key == 'Tab') {
                        e.preventDefault();
                        var start = this.selectionStart;
                        var end = this.selectionEnd;

                        this.value = this.value.substring(0, start) + "\t" + this.value.substring(end);

                        this.selectionStart = this.selectionEnd = start + 1;
                    }
                });
            }
        }
    };
</script>

<style scoped>
    .model {
        height: 500px;
        width: 98%;
        padding: 3px;
        border: 1px solid black;
    }

    .model textarea {
        width: 98%;
        height: 98%;
        margin: 0 auto;
        padding: 2px;
        resize: none;
        font-size: 16px;
        font-family: monospace;
    }
</style>