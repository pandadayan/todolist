<template>
    <footer>
        <ul>
          <li class="circle" 
            v-for = "tabbar in tabbars" 
            :key = " tabbar.id "
            :class = "[ tabbar.class,type == tabbar.text && 'circle-fill']"
            @click ="btnShow(tabbar.text)"
          >
            {{ tabbar.text }}
          </li>
        </ul>
      </footer>
</template>

<script>
export default {
    props:["type"],
    data(){
        return {
             tabbars: [
                {
                    id: 1,
                    text: 'A',
                    class: 'circle-success'
                },
                {
                    id: 2,
                    text: 'F',
                    class: 'circle-primary'
                },
                {
                    id: 3,
                    text: 'U',
                    class: 'circle-danger'
                }
            ],
        }
    },
    methods: {
        btnShow(i){
            this.$emit('get_tabbar',i)
        }
    },
}
</script>

<style>


</style>