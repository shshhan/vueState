<template>
    <div>
        <img @click="openModal(data.id)" :src="data.image" alt="roomImg" class="roomImg">
        <h4 @click="openModal(data.id)">{{data.title}}</h4>
        <p>{{data.price}}원</p>
        <!-- <button @click="increaseReportCnt(i)">허위매물신고</button>
        <span>신고수 : {{reportCnt[i]}} </span> -->
	</div>
  
</template>

<script>
export default {
name : 'Card',
props : {
  studioData : Object,
}
}
</script>

<style>
.roomImg {
  width : 100%;
  margin-top : 40px;
}
</style>