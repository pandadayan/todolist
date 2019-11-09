<template>
  <div>
      <div class="page-group">
        <div class="page page-current">
          
          <Header class="header" @input_flag = "input_flag"></Header>

          <Container @add_task = "add_task" :add_flag = "add_flag" :todos = "newdata" @del_task = "del_task"></Container>
          <Maskmy v-if = "mask_flag" :mask_flag = "mask_flag" @close_task = "close_task" @affirm_rem = "affirm_rem"></Maskmy>
        
          <Tabbar @get_tabbar = "get_tabbar" :type = "type"></Tabbar>
        </div>
      </div>
 
  </div>
</template>
<script>
import Header from '@/components/header'
import Container from '@/components/Container'
import Tabbar from '@/components/tabbar'
import Maskmy from '@/components/Maskmy'
export default {
  components:{
    Header,
    Container,
    Maskmy,
    Tabbar
  },
    data(){
      return {
        todos: [{
                id: 0,
                task: "任务一",
                done: true
            },
            {
                id: 2,
                task: "任务二",
                done: true
            }
        ],
        del_index: 0,
        mask_flag: false,
        add_flag: false,
        type:"A"

    }
    },
    computed: {
      newdata(){
        switch(this.type){
          case 'A':
            return this.todos
            break;
           case 'F':
            return this.todos.filter(item => item.done)
            break;
           case 'U':
            return this.todos.filter(item => !item.done)
            break;
        }
      }
    },
      created(){
        this.$http({
        url: 'http://localhost:3000/carouse',
        method:"post",
        params: {
          token: ''
        }
      }).then( res => {


        console.log(JSON.parse(res.data.split('&#34;').join('"')))
      })
        .catch( err => console.log( err ))
      },

    methods: {


        remove(index){
          this.todos.splice(index,1)
        },
        del_task(index){
          if(this.todos[index].done){
            this.remove(index)
          }else{
            this.del_index = index
            this.mask_flag = true
          }
        },

        close_task(){
          this.mask_flag = !this.mask_flag
        },
        affirm_rem(){
          this.remove(this.del_index)
          this.close_task()
        },
        //输入框显示隐藏
        input_flag(){
          this.add_flag = !this.close_taskadd_flag
        },
        add_task(data){
          console.log(sort(this.todos)[0])
          this.todos.unshift({
            id:sort(this.todos)[0].id+1,
            task:data,
            done:true
          })
        },
        get_tabbar(data){
          this.type = data
        }

    },

}
function sort(arr){
  return arr.sort(function(a,b){
    return b.id - a.id
  })
}
</script>

<style>
.header{
  overflow: hidden;
  height: 44px;
}
  .card-content-inner {
    overflow: hidden;
}

.btn-box {
    display: flex;
}

.btn-box button {
    margin-right: 10px;
}

.mask-box {
    position: fixed;
    left: 0;
    top: 0;
    z-index: 10000;
    width: 100%;
    height: 100%;
}

.mask-box .bg {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: black;
    opacity: .5;
}

.mask-content {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
    width: 80%;
    height: 110px;
    background: white;
    border-radius: 10px;
    padding: 10px;
    overflow: hidden;
}

.mask-content button {
    width: 80px;
    height: 30px;
    font-size: 14px;
}

.mask-content p {
    font-weight: bold;
}

.add {
    margin-top: 5px;
    margin-left: 10px;
}
*{
  margin: 0;
  padding: 0;
  list-style: none;
}

footer{
  position: fixed;
  left: 0; bottom: 0;

  width: 100%;
  height: 80px;
  border-top: 1px solid #ccc;
}

footer ul{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.circle{
  /* 这里写共用的样式 */
  width: 60px;
  height: 60px;

  color: #ccc;
  border: 1px solid #ccc; /* 默认边框 */
  text-align: center;
  line-height: 60px;

  border-radius: 50%;
}

.circle.circle-success{
  border-color: green;
  color: green;
}
.circle.circle-success.circle-fill{
  background: green;
  color: white;
}

.circle.circle-primary{
  border-color: blue;
  color: blue;
}
.circle.circle-primary.circle-fill{
  background: blue;
  color: white;
}

.circle.circle-danger{
  border-color: red;
  color: red;
}
.circle.circle-danger.circle-fill{
  background: red;
  color: white;
}
</style>
