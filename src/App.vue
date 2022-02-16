<template>
  <div class="menu">
		<a v-for="(name, i) in menuNames" :key="i">{{name}}</a>
  </div>

	<div v-for="(name, i) in products" :key="i">
		<h4>{{name}}</h4>
		<p>{{price[i]}}</p>
		<button v-on:click="increaseReportCnt(i)">허위매물신고</button>
		<span>신고수 : {{reportCnt[i]}} </span>
	</div>

</template>

<script>

export default {
  name: 'App',
  data(){
    return {  //데이터 보관함 
			menuNames : ['Home', 'Shop', 'About'],
      products : ['논현동원룸', '잠실동원룸', '가락동원룸'],
      price : [100, 90, 60],
      h4Color : 'color : blue',
			reportCnt : [0, 0, 0],
		}
  },
	methods :{
		increaseReportCnt(i){
			console.log(i + '번째 항목의 신고수가 1증가됩니다.');
			this.reportCnt[i]++;
		},
	},
  components: {
  }
}
</script>

<style>
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
