<template>
  <div>
    <transition-group name="list" tag="ul">
        <li v-for="(todoItem,index) in this.storedTodoItems" :key="todoItem.item" class="shadow">
            <i class="fas fa-check checkBtn" :class ="{checkBtnCompleted: todoItem.completed}" @click="toggleComplete({todoItem, index})"></i>
            <span :class="{textCompleted:todoItem.completed}">{{todoItem.item}}</span>
            
            <span class="removeBtn" @click="removeTodo({todoItem,index})">
                <i class="fas fa-trash" ></i>
            </span>
        </li>
    </transition-group>
  </div>
</template>

<script>
import{ mapGetters, mapMutations } from 'vuex'

export default {
    methods:{

        // 배열형으로 helper 선언
        // ...mapMutations(['removeOneItem','toggleOneItem']),
        
        //객체형 helper 선언 ( 이름을 다르게 할 경우)
        ...mapMutations({
            removeTodo: 'removeOneItem', // 인자들은 자동으로 넘긴다.
            toggleComplete: 'toggleOneItem'
        }),    

        /* helper 함수를 사용해 변경함.
        removeTodo(item){
            this.$store.commit('removeOneItem',item)
        },
        toggleComplete(todoItem, index){
            this.$store.commit('toggleOneItem',{todoItem, index})
        }
        */
    },

    computed:{
        ...mapGetters(['storedTodoItems'])
        // todoItems(){
        //     return this.$store.getters.storedTodoItems
        // }
        
    }
}
</script>

<style scoped>
ul{
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0px;
    text-align: left;
}
li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin:0.5rem 0;
    padding: 0 0.9rem;
    background:white;
    border-radius: 5px;
}
.checkBtn{
    line-height: 45px;
    color:#62acde;
    margin-right: 5px;
}
.checkBtnCompleted{
    color:#b3adad;
}
.textCompleted{
    text-decoration: line-through;
    color:#b3adad;
}
.removeBtn{
    margin-left: auto;
    color:#de4343
}
.list-enter-active, .list-leave-active {
transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
opacity: 0;
transform: translateY(30px);
}
/* 리스트 아이템 트랜지션 효과 */

.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>