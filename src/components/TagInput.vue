<script>
export default{
    props: ['modelValue'],
    data() {
        return {
            tagItems: [],
            tagInput: '',
            isEdit: true
        };
    },
    // --------
    methods: {
        updateData(ev) {
            ev.preventDefault()
            console.log('Coma added', this.tagInput);
            this.tagItems.push(this.tagInput);
            this.tagInput = ''
            this.$emit('update:modelValue', this.tagItems);
        },
        removeTag(){
            this.isEdit = false
        }
    }
}
</script>
<template>
    <div class="tag-input">
            <span class="tag" v-for="item in tagItems">&nbsp;{{ item  }}&nbsp;<span @click="removeTag"></span></span>
            <input type="text" class="" placeholder="Enter Variable Names" v-model="tagInput" @keypress.,="updateData"/>
    </div>
</template>
<style>

/* taginput---- */
.tag-input{
    padding: 10px 20px;
    border: 1px solid #ced4da;
    border-radius: 5px;
}
.tag-input .tag{
    display: inline-block;
    background-color: #212529;
    color: white;
    border-radius: 40px;
    padding: 2px 7px 2px 7px;
    margin-right: 5px;
    margin-bottom: 5px;
    /* line-height: 28px; */
}
.tag-input input{
    margin-bottom: 0;
    width: 150px;
    border: none;
}
.tag-input input:focus,
.tag-input input:focus-visible{
    border: none;
}
</style>
