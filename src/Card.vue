<template>
    <div>
        <img @click="openModalFromCompo(studio.id)" :src="studio.image" alt="roomImg" class="roomImg">
        <h4 @click="$emit('modalPop', studio.id)">{{studio.title}}</h4>
        <p>{{studio.price}}원</p>
        <!-- <button @click="increaseReportCnt(i)">허위매물신고</button>
        <span>신고수 : {{reportCnt[i]}} </span> -->
	</div>
  
</template>

<script>
export default {
  name : 'Card',
  props : {
    studio : Object,
  },
  methods : {
    openModalFromCompo(id){
      this.$emit('modalPop', id);
    },
  },
}
</script>

<style>
.roomImg {
  width : 100%;
  margin-top : 40px;
}
</style>