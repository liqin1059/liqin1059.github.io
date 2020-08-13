---
layout: post
title: Vue中使用 Swiper 
date: 2020-06-03 12:31:30
categories: vue
tags:
---

记录Vue中使用 Swiper 

<!-- more -->
# 包引入
> package.json文件引入包版本

```
"dependencies": {
  "swiper": "^5.3.0",
}
```
# tab-bar公共组件开发

## template
```
 <div class="lay-out">
  <div class="swiper-container" id="gallery">
    <div class="swiper-wrapper">
      <slot name="gallery"></slot> // 内容页
    </div>
  </div>
  <div class="swiper-container" id="thumbs">
    <div class="swiper-wrapper">
      <slot name="thumbs"></slot> // 底部导航
    </div>
  </div>
</div>
```
## 引入 
```
import Swiper from 'swiper';
import 'swiper/css/swiper.min.css';
```
## mounted钩子中初始化

- 这里是使用两个关联swiper实现左右滑动关联页面

```
this.$data.galleryBottom = new Swiper('#thumbs', {
    spaceBetween: 0,
    slidesPerView: 3,
    loop: false,
    freeMode: true,
    // loopedSlides: 4,
    watchSlidesVisibility: true,
    watchSlidesProgress: true,
    on: {
      touchEnd() {
        // console.log('当前的galleryBottom序号是' + this.activeIndex);
      }
    }
  });
  let self = this;
  this.$data.gallery = new Swiper('#gallery', {
    spaceBetween: 0,
    loop: false,
    observer: false,
    observeParents: false,
    // loopedSlides: 4,
    controller: {
      control: self.$data.galleryBottom
    },
    navigation: {
      nextEl: '#gallery .swiper-button-next',
      prevEl: '#gallery .swiper-button-prev'
    },
    thumbs: {
      swiper: self.$data.galleryBottom,
      slideThumbActiveClass: 'my-slide-thumb-active'
    },
    on: {
      touchEnd() {
        // console.log('当前的gallery序号是' + this.activeIndex);
      }
    }
  });
```
## 激活页面变化事件
- 在watch钩子函数中监听<b>activeIndex</b>变化
- <b>this.$data.gallery.activeIndex</b>当前激活页的序号(0-)
```
watch: {
  'gallery.activeIndex': 'indexChange'
}
```

# tab-bar公共组件引入页面

- 在引入之后我们需要在具名插槽渲染相应数量的<b>swiper-slide</b>

```
<tab-bar>
  <template v-slot:gallery>
    <div class="swiper-slide">
      <dealing @showOpinion="showOpinion"
              :rejectInfor="rejectInfor"
              :passInfor="passInfor"
              v-if="hasLogined"
              ref="dealingComponent">
      </dealing>
    </div>
    <div class="swiper-slide">
      <overdue v-if="hasLogined"></overdue>
    </div>
    <div class="swiper-slide">
      <fail v-if="hasLogined"></fail>
    </div>
  </template>
  <template v-slot:thumbs>
    <div class="swiper-slide swiper-after" v-for="(item, index) in tabData" :key="index">
      <span v-if="tabData.length - 1 !== index"></span>
      {{ item }}
    </div>
  </template>
</tab-bar>
```
