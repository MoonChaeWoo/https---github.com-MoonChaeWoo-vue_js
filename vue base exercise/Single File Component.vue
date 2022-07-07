<!-- 싱글 파일 컴포넌트 체계
   - 싱글 파일 컴포넌트 체계란 .vue 파일로 프로젝 구조를 구성하는 방식을 말한다.
   - 확장자 .vue 파일 1개는 뷰 애플리케이션을 구성하는 1개의 컴포넌트와 동일하다.
   - .vue 파일은 아래와 같은 구조를 가진다. -->
<template>
  <!-- <template>
          HTML 태그 내용         -> 화면에 표시할 요소들을 정의하는 영역 ex) HTML + 뷰 데이터 바인딩
       </template> -->

  <div>
    <span>
      <button>{{ message }}</button>
    </span>
  </div>
</template>

<script>
//  exprot default {
//    자바 스크립트 내용    -> 뷰 컴포넌트의 내용을 정의 하는 영역 ex) template, data, methods등
//  }
  export default {
    data : {
      message : 'click this button'
    }
  }

</script>

<style>
/* <style>
      css 스타일 내용      -> 템플릿에 추가한 HTML 태그의 CSS 스타일을 정의하는 영역
   </style>  */
span{font-size: 1.2em;}

</style>
