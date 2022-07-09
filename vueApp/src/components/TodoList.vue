<template lang="html">
  <section>
    <!-- transition-group은 ul태그 대신 사용하며 목록에 애니메이션을 추가할 때 사용되는 태그이다. -->
    <!-- tag이름은 애니메이션이 들어갈 HTML 태그이름 p, ul, section등 지정하면 된다. -->
    <!-- name속성은 이후에 추가할 CSS클래스와 연관이 있다. -->
    <transition-group name="list" tag="ul">
      <!-- key에 대한 이상적인 값은, 각 항목을 구별할 수 있는 유일한 값이어야 한다 -->
      <!-- v-bind:key -> :key
      v-on:click -> @click -->
      <!-- v-bind:key의 약식 :key이며 목록에 애니메이션을 적용하려면 transition-group 안의 대상 태그에
           :key 속성을 꼭 지정해야 한다. -->
      <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
        <i class="checkBtn fas fa-check" aria-hidden="true"></i>
        {{ todoItem }}
        <!-- @click은 v-on:click과 같은 의미이다. -->
        <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props : ['propsdata'],
  methods : {
    removeTodo(todoItem, index){
      // 로컬 스토리지에서 삭제를 하고 배열에서도 삭제를 해주어야한다.
      //localStorage.removeItem(todoItem);
      // todoItem의 배열 요소를 제거하자마자 바로 뷰에서 자동으로 화면을 다시 갱신한다.
      // 이는 데이터의 속성이 변하면 화면에 즉시 반영하는 뷰의 반응성 때문이다.
      //this.todoItems.splice(index,1);
      this.$emit('removeTodo', todoItem, index);
    }
  }
}
// localStorage 할 일 삭제
// (선택한 할 일을 뷰에서 인식) -> (선택한 할 일을 로컬 스토리지에서 삭제) -> (선택한 할 일을 뷰 데이터에서 삭제)
</script>

<style scoped>
  ul{list-style-type: none;padding-left: 0px;margin-top: 0;text-align: left;}
  li{display: flex;min-height: 50px;height: 50px;line-height: 50px;margin: 0 0.5rem 0; padding: 0 0.9rem; background: white; border-radius: 5px;}
  .checkBtn{line-height: 45px; color: #62acde; margin-right: 5px;}
  .removeBtn{margin-left: auto; color: #de4343;}


  /* transition-group의 name값의 list를 모두 접두사로 사용하고 있다. 데이터가 들어오고 나갈때 생기는 애니메이션 동작이
      enter-active 등등은 미리 정의되어있는거 같다. */
  .list-enter-active, .list-leave-active{
    transition: all 1s;
  }

  .list-enter, .list-leave-to{
    opacity: 0;
    transform: translateY(30px);
  }
</style>
