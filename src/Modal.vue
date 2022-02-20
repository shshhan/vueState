<template>
  <div class="black-bg" v-if="modalStatus">
    <div class="white-bg">
      <Discount/>
      <h4>{{studioData[studioId].title}}</h4>
      <p>{{studioData[studioId].content}}</p>
      <p>{{studioData[studioId].price}}원</p>
      <!-- <button @click="modalStatus = false">닫기</button> -->
    </div>
  </div>
</template>

<script>
export default {
name : 'Modal',
props : { //props는 readOnly
  studioData : Object,    //props로 받은 변수 : 자료형
  modalStatus : Boolean,
  studioId : Number,
}
}
</script>

<style>
.black-bg {
  width : 100%;
  height : 100%;
  background : rgba(0,0,0,0.5);
  position : fixed;
  padding : 20px;
}
.white-bg {
  width : 100%;
  background : white;
  border-radius : 8px;
  padding : 20px;
}
</style>