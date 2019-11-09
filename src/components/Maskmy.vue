<template>
     <div class="mask-box">
        <div class="bg"
        @click.self = "close_mask"
        ></div>
        <div class="mask-content">
        <p> 您真的确定要删除我吗？ </p>
        <button class="button button-primary button-fill pull-right"
        @click= "affirm_del"
        > 确定 </button>
        </div>
    </div>
</template>

<script>
export default {
    props:['mask_flag'],
    data(){
        return {
           
        }
    },
    methods: {
        close_mask(){
            this.$emit('close_task')
        },
        affirm_del(){
            this.$emit('affirm_rem')
        }
    },

}
</script>

<style scoped lang="stylus">

</style>
