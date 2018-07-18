<template>
    <form @submit.prevent="insertEmbed">
        <label>
            URL<br>
            <textarea ref="embedtxt" type="text" rows="4" cols="50" v-model="embedCode"></textarea>
        </label> 
        <br>
        <button type="submit">Insert Embed Code</button>
    </form>
</template>
<script>
    import bus from 'src/editor/bus.js';
    export default{
        title: 'embed',
        description: 'Insert your embed code',
        icon:'<svg width="500" height="500" viewBox="0 0 5 5" xmlns="http://www.w3.org/2000/svg"><path d="M133.333,116.667L0,250l133.333,133.333H200L66.667,250L200,116.667H133.333z M366.667,116.667H300L433.333,250L300,383.333h66.667L500,250L366.667,116.667z"/></svg>',
        props: {
            uid: null
        },
        data:function(){
            return{
                embedCode:''
            }            
        },
        methods:{
            insertEmbed:function(){
                this.$emit("exec", "insertHTML", this.embedCode);
                this.$parent.closeDashboard();
                this.embedCode='';
            }
        },
        created() {
        bus.on(this.uid + "_show_dashboard_embed", () => {
            this.$nextTick(() => {
                console.log('setting focus');
                this.$refs.embedtxt.focus();
            });
        });
    }
    }
</script>
<style>
</style>