<template>
  <div class="memo-app">
    <memo-form v-on:addMemo="addMemo"/>
      <ul class="memo-list">
        <memo v-for="memo in memos"
              :key="memo.id"
              :memo="memo"
              @deleteMemo="deleteMemo"
              @updateMemo="updateMemo" />
      </ul>
  </div>
</template>

<script>
import Memo from './Memo.vue';
import MemoForm from './MemoForm.vue';
export default {
  name: 'MemoApp',
  components:{
    Memo,
    MemoForm
  },
  data() {
    return {
      memos:[],
    }
  },
  created() {
    this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
  },
  methods: {
    addMemo(payload){
      this.memos.push(payload);
      this.storeMemo();
    },
    storeMemo(){
      const memoToString = JSON.stringify(this.memos);
      localStorage.setItem('memos', memoToString);
    },
    deleteMemo(id){
      const targetIndex = this.memos.findIndex(v => v.id === id);
      this.memos.splice(targetIndex, 1);
      this.storeMemo();
    },
    updateMemo(payload){
      const {id, content} = payload;
      const targetIndex = this.memos.findIndex(v => v.id === id);
      const targetMemo = this.memos[targetIndex];
      this.memos.splice(targetIndex, 1, {...targetMemo, content});
      this.storeMemo();
    }
  },
};
</script>

<style scoped>
.app-header{
    overflow: hidden;
    padding: 52px 0 27px;
}
.app-header h1{
    float:left;
    font-size: 24px;
    text-align: center;
}

.memo-list{
  padding: 20px 0;
  margin: 0;
}

</style>
