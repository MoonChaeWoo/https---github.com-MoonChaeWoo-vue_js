<template lang="html">
  <div class="inputBox shadow">
    <!-- 엔터를 누르면 addTodo 메소드가 실행될 수 있도록 해준다. -->
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">
        할 일을 입력하세요
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>

  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  props : ['propsdata'],
  data : () => ({
    newTodoItem : '',
    showModal : false
  }),
  methods : {
    // 입력받은 텍스트를 로컬 스토리지에 저장
    // 1. setItem() API를 이용하여 저장한다. setItem()은 로컬 스토리지에 데이터를 추가하는 API이다.
    // 2. API 형식은 키, 값 형태이며 저장 기능을 최대한 단순하게 하기 위해 키, 값 모두 입력받은 텍스트로 지정한다.

    // 로컬스토리지 다루기
    // 1. localStorage.setItem(key, value); : 로컬 스토리지에 저장
    // 2. localStorage.getItem(key) : 데이터 조회
    // 3. localStorage.removeItem(key) : 키에 해당하는 데이터 삭제
    // 4. localStorage.clear() : 저장소 데이터 전체 삭제
    addTodo(){
      // 개발도구 → application → Storage → localStorage → url에 들어가면 저장된 정보를 볼 수 있다.
      // sesssionStorage.setItem()을 한다면 세션 스토리지에 저장이 된다.
      //localStorage.setItem(this.newTodoItem, this.newTodoItem)
      if(this.newTodoItem !== ""){
        //localStorage.setItem(this.newTodoItem, this.newTodoItem);
        //console.log(localStorage.getItem(this.newTodoItem));
        var value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit('addTodo', value);
        this.clearInput();
      }else {
        alert('none');
        this.showModal = !this.showModal;
      }
    },
    clearInput(){
      this.newTodoItem='';
    }
  },
  components : {
    'Modal' : Modal
  }
}
</script>

<style scoped>
  input:focus{outline:none;}
  .inputbox{background:white;height:50px;line-height:50px;border-radius:5px;}
  .inputbox input{border-style:none;font-size:0.9rem;}
  .addContainer{float:right;background:linear-gradient(to right, #6478FB, #8763FB);display:block;width:3rem;border-radius:0 5px 5px 0;}
  .addBtn{color: white;vertical-align:middle;}

</style>
