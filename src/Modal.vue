<template>
  <div class="black-bg" v-if="modalStatus">
    <div class="white-bg">
      <Discount/>
      <h4>{{studioData[studioId].title}}</h4>
      <p>{{studioData[studioId].content}}</p>
      <p>{{studioData[studioId].price}}원/월</p>
      <div>
        <input @input="month = $event.target.value">  <!-- addEventlistner('input', function(e){ month = e.target.value}) 와 같음 -->
        <!-- 여기엔 값을 입력하면 month에 값이 대입, month의 값이 변해도 이 input은 그대로-->
      </div>
      <div>
        <input v-model.number="month">  <!-- input value는 항상 문자열, v-model.데이터타입="**" 하면 해당 데이터 타입으로 value 받음-->
        <!-- 여기엔 값을 입력하면 month와 동기화(?)-->
      </div>
      <div>
        <textarea v-model="string" cols="30" rows="10"></textarea>
      </div>
      <select v-model.number="month">
        <option>1</option>
        <option>2</option>
        <option>3</option>
        <option>4</option>
        <option>5</option>
      </select>
      <div>
        <input type="checkbox" v-model="true_false">
      </div>
      <input type="range" min="1" max="12">
      <p>{{ month }}개월 : {{studioData[studioId].price + month}}원</p>
      <p>{{ string }}</p>
      <p v-if="true_false">체크박스 선택함</p>
      <button @click="$emit('modalClose')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
name : 'Modal',
data(){
  return{
    month : 0,
    string : '',
    true_false : false,
  }
},
watch : { //watcher : input value 확인
  month(postVal) { //data의 month가 변경될 때 마다 value 체크
    const regex = /[^0-9]/g;

    if(regex.test(postVal)){
      alert('숫자만 입력 가능합니다.');
      this.month = postVal.replace(regex,'');
    }
  
    if(postVal > 12){
      alert('12개월 이하로 설정하세요');
    }

  },
},
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