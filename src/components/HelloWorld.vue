<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <Button v-on:click="onclick">点我</Button>
        <quill-editor
                :options="editorOption"
                @blur="onEditorBlur($event)"
                @focus="onEditorFocus($event)"
                @ready="onEditorReady($event)"
                ref="myQuillEditor"
                v-model="content"
        />

        <p>预览：</p>
        <div class="ql-container ql-snow">

            <div class="ql-editor" v-html="content">
                {{content}}
            </div>

        </div>


    </div>
</template>

<script>
    import 'quill/dist/quill.snow.css'

    import {quillEditor} from 'vue-quill-editor'

    export default {
        components: {
            quillEditor
        },
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                content: '<h2>I am Example</h2>',
                contentResolved: '',
                editorOption: {
                    // Some Quill options...
                }
            }
        },
        methods: {
            onEditorBlur(quill) {
                console.log('editor blur!', quill)
            },
            onEditorFocus(quill) {
                console.log('editor focus!', quill)
            },
            onEditorReady(quill) {
                console.log('editor ready!', quill)
            },
            onEditorChange({quill, html, text}) {
                console.log('editor change!', quill, html, text)
                this.content = html
            },
            onclick(e) {
                e.preventDefault();
                console.log(this.content);
                // this.contentResolved = this.content;
                let abc = this.$refs['myQuillEditor'];
                console.log(abc)

            }
        },
        computed: {
            editor() {
                return this.$refs.myQuillEditor.quill
            }
        },
        mounted() {
            console.log('this is current quill instance object', this.editor)
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
