<template>
  <Modal v-bind:studioData="studioData" :modalStatus="modalStatus" :studioId="studioId" @modalClose="modalStatus=false"/>
  <!-- v-bind:는 : 기호와 같음,
  아래에 선언되어 있는 변수가 아닌 Array나 Object등 데이터를 바로 쓸 수 도 있음,
  문자열을 보낼 때는 v-bind없이도 보낼 수 있음 -->
  <div class="menu">
		<a v-for="(name, i) in menuNames" :key="i">{{name}}</a>
  </div>
  <Discount/> 
  <Discount></Discount>
  <Card @modalPop="openModal($event)" :data="studioData[i]" v-for="(data, i) in studioData" :key="data"/>
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
      studioId : 0,                     
      h4Color : 'color : blue',
			reportCnt : [0, 0, 0],
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
    }
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
</style>
