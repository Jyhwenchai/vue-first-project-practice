<script setup>
import { formatDate } from 'common/utils'

defineProps({
  commentInfo: {
    type: Array,
    default () {
      return []
    }
  }
})

function showDate (value) {
  // 将时间戳转换成date对象
  const date = new Date(value * 1000)
  // 将date进行格式化
  return formatDate(date, 'yyyy-MM-dd')
}

</script>

<template>
<div v-if="Object.keys(commentInfo).length !== 0" class="comment-info-wrap" >
  <div class="comment-title flex">
    <div>用户评价</div>
    <div>更多</div>
  </div>
  <div v-for="(item, index) in commentInfo" :key="index">
    <div class="comment-user-info">
      <span><img :src="item.user.avatar" alt="" class="avatar"></span>
      <span>{{item.user.uname}}</span>
    </div>
    <div class="comment-text">{{item.content}}</div>
    <div class="comment-goods-info">
      <span class="comment-time">{{showDate(item.created)}}</span>
      <span>{{item.style}}</span>
    </div>
    <div class="flex">
      <div v-for="(image, idx) in item.images" :key="idx" class="comment-info-images" >
        <img :src="image" alt="">
      </div>
    </div>
  </div>
</div>
</template>

<style scoped>
.comment-info-wrap {
  padding: 0 8px;
  font-size: 14px;
  border-bottom: 4px solid #ececec;
}

.comment-info-wrap .comment-title {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #ececec;
  padding: 10px 4px;
}

.comment-user-info {
  padding: 10px 0;
}

.comment-user-info .avatar {
  width: 40px;
  height: 40px;
  border-radius: 100%;
  margin-right: 10px;
  vertical-align: middle;
}

.comment-text {
  line-height: 20px;
}

.comment-goods-info {
  color: #999;
  margin: 4px 0;
}

.comment-goods-info .comment-time {
  margin-right: 10px;
}

.comment-info-images img {
  width: 60px;
  height: 60px;
  margin-right: 6px;
}

</style>
