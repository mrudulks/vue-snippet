<script>
import TagInput from './TagInput.vue'
export default {
    // components:{
    //     'tag-input': TagInput,
    // },
    // template:'#input-elements',
    components:{
        TagInput
    },
    props:['on-item-saved'],
    data(){
        return{
            codeName:'',
            codeLanguage:'',
            codeContent:'',
            name:''
        }
    },
    methods:{
        addElements() {
            fetch('http://0.0.0.0:5000/snippets', {
                method: "post",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    codename: this.codeName,
                    codelanguage: this.codeLanguage,
                    codecontent: this.codeContent,
                    variables:this.name
                
                })
            })
        this.$emit('created' );
        }
    }
}
</script>
<template>

    <div class="container"  >
    <h3 class="text-center">Add Elements</h3>
                    <div class="row justify-content-center" >
        <div class="col-md-8 mt-5">
            <input type="text" v-model="codeName" class="form-control" placeholder="Name">
            <input type="text" v-model="codeLanguage" class="form-control" placeholder="Language">
            <tag-input v-model="name"></tag-input>
            <!-- <tag-input   ></tag-input> -->
                <div class="text-area" >
                    <textarea name="" id="" rows="10" class="form-control" placeholder="Write Your code" v-model="codeContent"></textarea>
                </div>
            <div class="text-left pt-2" style="text-align: right;">
                <button @click="addElements()" class="btn btn-dark">Add Code</button>
            </div>
        </div>
    </div>
                    <!-- <input-elements @created="snippetFetch" ></input-elements>   -->
                </div>

    
</template>
