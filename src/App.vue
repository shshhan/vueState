<template>

  <div class="black-bg" v-if="modalStatus">
    <div class="white-bg">
      <h4>{{studios[studioId].title}}</h4>
      <p>{{studios[studioId].content}}</p>
      <p>{{studios[studioId].price}}원</p>
      <button @click="modalStatus = false">닫기</button>
    </div>
  </div>

  <div class="menu">
		<a v-for="(name, i) in menuNames" :key="i">{{name}}</a>
  </div>

	<div v-for="(data, i) in studios" :key="i">
    <img :src="data.image" alt="roomImg" class="roomImg">
		<h4 @click="openModal(data.id)">{{data.title}}</h4>
		<p>{{data.price}}원</p>
		<!-- <button @click="increaseReportCnt(i)">허위매물신고</button>
		<span>신고수 : {{reportCnt[i]}} </span> -->
	</div>

</template>

<script>

import studioData from './assets/studio.js';

export default {
  name: 'App',
  data(){
    return {  //데이터 보관함 
      modalStatus : false,
			menuNames : ['Home', 'Shop', 'About'],
      studios : studioData,
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

.roomImg {
  width : 100%;
  margin-top : 40px;
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
