<template>
  <li class="memo-item">
    <strong>{{memo.title}}</strong>
    <p @dblclick="handleDblClick">
      <template v-if="!isEditing">{{memo.content}}</template>
      <input
        v-else
        type="text"
        ref="content"
        :value="memo.content"
        @blur="handleBlur"
        @keydown.enter="updateMemo"
      />
    </p>
    <button type="button" @click="deleteMemo">
      <i class="fas fa-times"></i>
    </button>
  </li>
</template>

<script>
export default {
  beforeUpdate() {
    console.log("beforeUpdate=>", this.$refs.content);
  },
  updated() {
    console.log("updated", this.$refs.content);
  },
  data() {
    return {
      isEditing: false
    };
  },
  name: "Memo",
  methods: {
    deleteMemo() {
      const id = this.memo.id;
      this.$emit("deleteMemo", id);
    },
    handleDblClick() {
      this.isEditing = true;
      console.log("beforeUpdate=>", this.$refs.content);
      this.$nextTick(() => {
        this.$refs.content.focus();
      });
    },
    updateMemo(e) {
      const id = this.memo.id;
      const content = e.target.value.trim();
      if (content.length <= 0) {
        return false;
      }
      this.$emit("updateMemo", { id, content });
      this.isEditing = false;
    },
    handleBlur() {
      this.isEditing = false;
    }
  },
  props: {
    memo: {
      type: Object
    }
  }
};
</script>

<style scoped>
.memo-item {
  overflow: hidden;
  position: relative;
  margin-bottom: 20px;
  padding: 24px;
  box-shadow: 0 4px 10px -4px rgba(0, 0, 0, 0.2);
  background-color: #1969ab1d;
  list-style: non;
}

.memo-item:hover {
  background-color: #6bbcff8e;
  transition: 1s;
}

.memo-item button {
  background: none;
  position: absolute;
  right: 20px;
  top: 20px;
  font-size: 20px;
  color: #e5e5e555;
  border: 0;
}

.memo-item strong {
  display: block;
  margin-bottom: 12px;
  font-size: 18px;
  font-weight: normal;
  word-break: break-all;
}
.memo-item p {
  margin: 0;
  font-size: 14px;
  line-height: 22px;
  color: #666;
}

.memo-item p input[type="text"] {
  box-sizing: border-box;
  width: 100%;
  font-size: inherit;
  border: 1px solid #666;
}

a {
  position: relative;
  display: inline-block;
  padding: 15px 30px;
  color: #2196f3;
  text-transform: uppercase;
  letter-spacing: 4px;
  text-decoration: none;
  font-size: 24px;
  overflow: hidden;
  transition: 0.2s;
}
a:hover {
  color: #255784;
  background: #2196f3;
  box-shadow: 0 0 10px #2196f3, 0 0 40px #2196f3, 0 0 80px #2196f3;
  transition-delay: 1s;
}
a span {
  position: absolute;
  display: block;
}
a span:nth-child(1) {
  top: 0;
  left: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, #2196f3);
}
a:hover span:nth-child(1) {
  left: 100%;
  transition: 1s;
}
a span:nth-child(3) {
  bottom: 0;
  right: -100%;
  width: 100%;
  height: 2px;
  background: linear-gradient(270deg, transparent, #2196f3);
}
a:hover span:nth-child(3) {
  left: 100%;
  transition: 1s;
  transition-delay: 0.5s;
}
a span:nth-child(2) {
  top: -100%;
  right: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(180deg, transparent, #2196f3);
}
a:hover span:nth-child(2) {
  top: 100%;
  transition: 1s;
  transition-delay: 0.25s;
}
a span:nth-child(4) {
  bottom: -100%;
  left: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(360deg, transparent, #2196f3);
}
a:hover span:nth-child(4) {
  bottom: 100%;
  transition: 1s;
  transition-delay: 0.75s;
}
</style>
