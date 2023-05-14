<template>
  <form action="/">
      <van-search
          v-model="searchText"
          show-action
          placeholder="请输入要搜索的标签"
          @search="onSearch"
          @cancel="onCancel"
      />
  </form>
  <van-divider :show="true" content-position="left">已选标签</van-divider>
  <div v-if="activeIds.length === 0">请选择标签</div>
  <van-row gutter="16" style="padding: 0 16px">
      <van-col v-for="tag in activeIds">
          <van-tag  closeable size="small" type="primary" @close="doClose(tag)">
              {{ tag }}
          </van-tag>  
      </van-col>
  </van-row>

  <van-divider content-position="left">选择标签</van-divider>
  <van-tree-select
      v-model:active-id="activeIds"
      v-model:main-active-index="activeIndexs"
      :items="tagList"
  />
  <div>
      <van-button block type="primary" @click="doSearchResult" style="margin: 12px">
          搜索
      </van-button>
  </div>

</template>

<script setup>
import { ref } from 'vue'
import { showToast } from 'vant'
const searchText = ref('');
const originTagList = [{
      text: '性别',
      children: [
          { text: '男', id: '男' },
          { text: '女', id: '女' },
      ],
  },{
      text: '年级',
      children: [
          { text: '大一', id: '大一' },
          { text: '大二', id: '大二' },
          { text: '大三', id: '大三' },
          { text: '大四', id: '大四' },
          { text: '研一', id: '研一' },
          { text: '研二', id: '研二' },
      ],
  },
];
let tagList = ref(originTagList);

const onSearch = (val) => {
  tagList.value = originTagList.map(parentTag => {
      const tempChildren = [...parentTag.children];
      const tempParentTag = {...parentTag};
      tempParentTag.children = tempChildren.filter(item => item.text.includes(searchText.value));
      return tempParentTag;
  });
};
const onCancel = () => {
  searchText.value = '';
  tagList.value = originTagList;
};
//已选中的标签
const activeIds = ref(['男', '女']);
const activeIndexs = ref(0);

const doClose = (tag) => {
  activeIds.value = activeIds.value.filter(item => {
      return item !== tag;
  })
}

</script>

<stype scoped>
</stype>