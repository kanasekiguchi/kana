<template>
  <div id="headerSection">
    <input
      id="nav-input"
      v-model="check"
      type="checkbox"
      class="nav-unshown"
    >
    <label
      id="nav-open"
      for="nav-input"
    >
      <img
        class="headerButton"
        src="@/assets/menu3.png"
      >
    </label>
    <label
      id="nav-close"
      class="nav-unshown"
      for="nav-input"
    />
    <div id="nav-content">
      <Menu @close="closeDrower" />
    </div>
  </div>
</template>

<script>
 import Menu from './Menu.vue'
 export default {
  name: 'App',
  components: {
    Menu
  },

  data(){
    return {
      check: false
    }
  },
  methods:{
    closeDrower(){
      this.check= false
    }
  }
}

</script>

<style scoped>
/* ヘッダーまわりはサイトに合わせて調整してください */
#headerSection {
  background-color: #f3f3f3;
  width: 100%;
  height: 35px;
}

#nav-drawer {
  position: relative;
}

/* チェックボックス等は非表示に */
.nav-unshown {
  display: none;
}

/* アイコンのスペース */
#nav-open {
  display: inline-block;
  width: 30px;
  height: 22px;
  vertical-align: middle;
}

/* ハンバーガーアイコンをCSSだけで表現 */
#nav-open span,
#nav-open span::before,
#nav-open span::after {
  position: absolute;
  height: 3px;/* 線の太さ */
  width: 25px;/* 長さ */
  border-radius: 3px;
  background: #555;
  display: block;
  content: '';
  cursor: pointer;
}

#nav-open span::before {
  bottom: -8px;
}

#nav-open span::after {
  bottom: -16px;
}

/* 閉じる用の薄黒カバー */
#nav-close {
  display: none;/* はじめは隠しておく */
  position: fixed;
  z-index: 99;
  top: 0;/* 全体に広がるように */
  left: 0;
  width: 100%;
  height: 100%;
  background: black;
  opacity: 0;
  transition: 0.3s ease-in-out;
}

/* 中身 */
#nav-content {
  overflow: auto;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;/* 最前面に */
  width: 90%;/* 右側に隙間を作る（閉じるカバーを表示） */
  max-width: 250px;/* 最大幅（調整してください） */
  height: 80%;
  background: #fff;/* 背景色 */
  transition: 0.3s ease-in-out;/* 滑らかに表示 */
  -webkit-transform: translateX(-105%);
  transform: translateX(-105%);/* 左に隠しておく */
}

/* チェックが入ったらもろもろ表示 */
#nav-input:checked ~ #nav-close {
  display: block;/* カバーを表示 */
  opacity: 0.5;
}

#nav-input:checked ~ #nav-content {
  -webkit-transform: translateX(0%);
  transform: translateX(0%);/* 中身を表示（右へスライド） */
  box-shadow: 6px 0 25px rgba(0, 0, 0, 0.15);
}

.headerButton {
  width: 38px;
  cursor: pointer;
}

</style>
