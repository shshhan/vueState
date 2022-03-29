<template>

  <!-- <div class="start" :class="{end : modalStatus}"> -->
    <transition name="fade">  
      <Modal v-bind:studioData="studioData" :modalStatus="modalStatus" :studioId="studioId" @modalClose="modalStatus=false"/>
      <!-- v-bind:는 : 기호와 같음,
      아래에 선언되어 있는 변수가 아닌 Array나 Object등 데이터를 바로 쓸 수 도 있음,
      문자열을 보낼 때는 v-bind없이도 보낼 수 있음 -->  
    </transition>
  <!-- </div> -->

  <div class="menu">
		<a v-for="(name, i) in menuNames" :key="i">{{name}}</a>
  </div>

  <Discount /> 

  <button @click="priceFromLowToTop()">낮은 가격순으로 보기</button>
  <button @click="priceFromTopToLow()">높은 가격순으로 보기</button>
  <button @click="sortBack()">원래 정렬로 돌아가기</button>


  <Card @modalPop="openModal($event)" :studio="studioData[i]" v-for="(data, i) in studioData" :key="i"/>

  <!-- <Card :data="studioData[1]"/>
  <Card :data="studioData[2]"/>
  <Card :data="studioData[3]"/>
  <Card :data="studioData[4]"/>
  <Card :data="studioData[5]"/> -->
	<!-- <div v-for="(data, i) in studioData" :key="i">
    <img @click="openModal(data.id)" :src="data.image" alt="roomImg" class="roomImg">
		<h4 @click="openModal(data.id)">{{data.title}}</h4>
		<p>{{data.price}}원</p>
		<button @click="increaseReportCnt(i)">허위매물신고</button>
		<span>신고수 : {{reportCnt[i]}} </span>
	</div> -->

</template>

<script>

import studioData from './assets/studio.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data(){     //데이터를 쓰는 곳이 여러군데라면 되도록 부모 컴포넌트에 데이터를 만드는 것이 좋음
    return {  //데이터 보관함 
      modalStatus : false,
			menuNames : ['Home', 'Shop', 'About'],
      studioData,
      studioDataOriginal : [...studioData], 
        //sort하면 원본 데이터의 손상이 발생하기 때문에 사본 데이터를 저장.
        //... 연산자는 object나 array의 바깥 괄호를 제거해주어 안에 값만 복사한다.
        //등호 연산자로 가져오면 객체의 주소가 복사되어 값이 공유되는 것을 막기위해 ...으로 바깥 괄호를 없애고 다시 씌워주면 값을 복사해올 수 있다. 
      studioId : 0,                     
      h4Color : 'color : blue',
			reportCnt : [0, 0, 0],
      discountRate : 40,
		}
  },
	methods :{
		increaseReportCnt(i){
			console.log(i + '번째 항목의 신고수가 1증가됩니다.');
			this.reportCnt[i]++;
		},

    openModal(id){
      this.modalStatus = true;
      this.studioId = id;
    },

    priceFromLowToTop(){
      this.studioData.sort(function(a, b){
        return a.price - b.price;
      });
      // sort를 사용하면 원본 데이터도 손상된다.
    },

    priceFromTopToLow(){
      this.studioData.sort(function(a, b){
        return -(a.price - b.price);
      });
    },

    sortBack(){
      this.studioData = [...this.studioDataOriginal];
    },
	},

  components: {
    Discount, //discount : discount는 discount라고만 써도 가능. ES6신문법
    Modal,
    Card,
  }
}
</script>


<style>
body {
  margin : 0;
}
div {
  box-sizing : border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}
.menu{
  background: darkslateblue;
  padding : 15px;
  border-radius: 5px;
}
.menu a{
  color : white;
  padding : 10px;
}
.start {
  opacity: 0;
  transition : all 1s;
  /* transition : 모든 속성이 변할 때의 속성*/
}
.end {
  opacity: 1;
}
.fade-enter-from { /* 시작 스타일링 */
	transform: translateY(-1000px);
}
.fade-enter-active{ /* 트랜지션 */
  transition: all 1s;
}
.fade-endter-to{ /* 끝 스타일링 */
	transform: translateY(0px);
}
.fade-leave-from { /* 시작 스타일링 */
  opacity: 1;
}
.fade-leave-active{ /* 트랜지션 */
  transition: all 1s;
}
.fade-leave-to{ /* 끝 스타일링 */
  opacity: 0;
}

</style>