
<template>
  <van-nav-bar title="标题" right-text="按钮" left-arrow @click-left="onClickLeft" @click-right="onClickRight">
    <template #right>
      <van-icon name="search" size="18" />
    </template>
  </van-nav-bar>

  <div id="content">
    <router-view />
  </div>
  <router-link to="/">Go to Home</router-link>
  <router-link to="/team">队伍</router-link>
  <van-tabbar route v-model="active" @change="onChange">
    <van-tabbar-item to="/" icon="home-o" name="index">主页</van-tabbar-item>
    <van-tabbar-item to="/team" icon="search" name="team">队伍</van-tabbar-item>
    <van-tabbar-item to="/user" icon="friends-o" name="user">个人</van-tabbar-item>
  </van-tabbar>
</template>

<script setup>
import { ref } from 'vue';
import { showToast } from 'vant';
const onClickLeft = () => alert('left');
const onClickRight = () => alert('right');
const active = ref("index");
const onChange = (index) => showToast(`标签 ${index}`);
</script>

<style scoped></style>