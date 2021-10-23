<script>
    import {CodeMirror} from 'vue-codemirror'
    import 'codemirror/lib/codemirror.css'
    import 'codemirror/theme/dracula.css'
    // import 'codemirror/mode/xml/xml.js'
    import 'codemirror/mode/javascript/javascript'
    export default { 
        props: ['compitem'],
        data() {
            return {
                codeRender: _.template(this.compitem.codecontent),
                id: '',
                codeVariables: {}
            }
        },
        methods: {

            renderCode() {
                //             console.log("my array",this.compitem[1])
                this.compitem;

                // console.log("New Temp",this.codeRender)
                var defaultData = {};
                // console.log('renderTemplate', this.compitem + '');
                for (var i in this.compitem.variables) {
                    defaultData[this.compitem.variables[i]] = ''
                }
                try {
                    return this.codeRender(Object.assign(defaultData, this.codeVariables));
                } catch (e) {
                    console.log('Error', e)
                }

            }
        },
        mounted(){
            CodeMirror.fromTextArea(document.getElementById('editor'),{
                lineNumbers:true,
                theme:"dracula",
                mode:"javascript"
            })
        }
    }
</script>
<template>

    <div class="row">
        <div class="col-md-12">
            <h3 class="text-center">Code Render</h3>
        </div>
        <div class="col-md-6 mt-5">
            <div class="rendered-elements">
                <h3>{{ compitem.codename }}</h3>
                <p>{{ compitem.codelanguage }}</p>
                <input type="text" class="form-control" placeholder="Enter Variable Name"
                    v-for="ele in compitem.variables" v-model="codeVariables[ele]">
            </div>
            <button class="btn btn-dark mt-5" @click="selectedItem = null">Back to list</button>
        </div>
        <div class="col-md-6 mt-5">
            <div class="rendered-code">
                <h4>Code</h4>
                <!-- <pre>
                        {{ renderCode() }}
                </pre> -->
                <textarea name=""  cols="30" rows="10" id="editor">  {{ renderCode() }}</textarea>
            </div>
        </div>
    </div>




</template>

<style scoped>
    /* code editor */
    input[type="text"] {
        margin-bottom: 1rem;
    }

    .text-area {
        padding: 10px;
        background-color: #f8f9fa;
        border-radius: 5px;
        margin-top: 1rem;
    }

    /* Render Elemnets */
    .rendered-elements {
        padding: 30px 20px;
        background-color: #6a6969;
        color: white;
        height: 100%;
    }

    .rendered-elements h3 {
        text-transform: capitalize;
    }

    .rendered-elements p {
        font-size: 18px;

    }

    .rendered-elements,
    .rendered-code {
        border-radius: 10px;
    }

    .rendered-code {
        background-color: #f8f9fa;
        padding: 30px 20px;
    }

    .rendered-code pre {
        padding: 20px 15px;
        margin-bottom: 0;
        min-height: 150px;
    }

    .footer-main {
        background-color: #212529;
        position: fixed;
        bottom: 0;
        width: 100%;
    }
</style>