<template>
    <header class="bar bar-nav">
        <a class="icon icon-left pull-left"></a>
        <i class="icon icon-edit pull-right"
        @click = "add"
        ></i>
        <h1 class="title"> MMR </h1>
    </header>
</template>

<script>

export default {
  data(){
      return {}
  },
  methods: {
    add(){
      this.$emit('input_flag')
    }
  },

}
</script>

<style>

</style>
