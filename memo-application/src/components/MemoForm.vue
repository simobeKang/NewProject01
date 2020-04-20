<template>
  <div class="memo-form link-1">
    <form @submit.prevent="addMemo">
      <fieldset>
        <div class="memo-ligtfom">
          <a>
            <input
              class="memo-form__title-form"
              type="text"
              v-model="title"
              placeholder="メモ―の題目を入力してください"
            />
          </a>
          <a>
            <textarea
              class="memo-form__content-form"
              v-model="content"
              placeholder="メモ―の内容を入力してください"
            />
          </a>
          <button type="reset">
            <i class="fas fa-sync-alt"></i>
          </button>
        </div>
        <button type="submit">✔</button>
      </fieldset>
    </form>
  </div>
</template>

<script>
export default {
  name: "MemoForm",
  data() {
    return {
      title: "",
      content: ""
    };
  },
  methods: {
    resetFields() {
      this.title = "";
      this.content = "";
    },
    addMemo() {
      //비구조화 할당 구문을 이용 변수를 선언
      const { title, content } = this;
      // const id = new Date().getTime();

      const isEmpty = title.length <= 0 || content.length <= 0;
      if (isEmpty) {
        return false;
      }

      //this.$emit('addMemo', {id, title, content});
      this.$emit("addMemo", { title, content });
      this.resetFields();
    }
  }
};
</script>

<style scoped>
.memo-form {
  margin-bottom: 24px;
  padding-bottom: 40px;
}

[class^="link-1"] {
  display: inline-block;
  margin: 2em;
}

a {
  text-transform: uppercase;
  font-size: 36px;
  color: white;
  text-decoration: none;
  position: relative;
  display: block;
}

/* linkone */
.link-1 a:before,
.link-1 a:after {
  content: "";
  border-bottom: solid 1px #2196f3;
  position: absolute;
  bottom: 0;
  width: 0;
}

.link-1 a:before {
  left: 0;
}
.link-1 a:after {
  right: 0;
}

.link-1 a:hover:before,
.link-1 a:hover:after {
  width: 50%;
}

.link-1 a:before,
.link-1 a:after {
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
}

fieldset {
  border-width: 0px !important;
  text-align: center;
}
.memo-form form fieldset div {
  position: relative;
  padding: 24px;
  margin-bottom: 20px;
}

.memo-form form fieldset div button[type="reset"] {
  position: absolute;
  right: 20px;
  bottom: 20px;
  font-size: 16px;
  background: none;
  color: #877f7faf;
}

.memo-form form fieldset button[type="submit"] {
  float: right;
  width: 40px;
  padding: 12px 0;
  border-radius: 4px;
  font-size: 10px;
  background-color: #f85151;
  color: aquamarine;
  letter-spacing: 4px;
  text-decoration: none;
  overflow: hidden;
  transition: 0.2s;
}

button[type="submit"]:hover {
  box-shadow: 10px 0 10px #f85151, 0 0 0px #f85151, 0 0 10px #f85151;
  transition-delay: 0s;
}

.memo-form form fieldset .memo-form__title-form {
  width: 100%;
  margin-bottom: 12px;
  font-size: 18px;
  line-height: 26px;
  color: rgba(255, 255, 255, 0.721);
  background: #031321;
}

.memo-form form fieldset .memo-form__content-form {
  width: 100%;
  height: 66px;
  font-size: 14px;
  line-height: 22px;
  vertical-align: top;
  color: rgba(255, 255, 255, 0.721);
  background: #031321;
}

.memo-form input:focus {
  outline: none;
}

textarea:focus {
  outline: none;
}

.memo-ligtfom:hover {
  box-shadow: 10px 0 20px #2196f3, 0 0 20px #2196f3, 0 0 10px #2196f3;
  transition-delay: 0s;
}
</style>
