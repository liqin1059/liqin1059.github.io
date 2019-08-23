---
layout: post
title: vue拖拽插件vuedraggable
date: 2019-08-30 16:31:30
categories: vue
tags: [draggable]
description: vue拖拽插件vuedraggable
---



## 安装
```
npm install vuedraggable -s
```
## 引入

```
import draggable from 'vuedraggable';
```

## 组件中声明
```
components: {
  draggable
}
```

## 使用

- 在vue需要拖拽的列表外层使用（目前是两个列表中拖拽生成）
* 第一个拖拽列表

```
<draggable
    class="dragArea list-group"
    :group="{ name: 'componentsData', pull: 'clone', put: false }" // 拖拽对象data,是否克隆，是否可放置
    :sort="false" // 是否排序
    :value="componentsData" // 拖拽对象data
    dragClass="dragClass"
    @change="log" // 发生拖拽变化时
  >
    <div v-for="(item, index) in componentsData"
        :key="index"
        draggable="true"
        class="drag-list">
        <span class="iconfont" :class="item.icon"></span>
        <p class="name">{{ item.name }}</p>
    </div>
</draggable>
```
* 第二个拖拽列表

```
<draggable
  class="dragArea list-group"
  :group="{ name: 'componentsData', put: true }"
  :value="putList"
  ghostClass="ghostClass" // 拖拽样式
  chosenClass="chosenClass" // 选中的样式
  dragClass="dragClass" // 选中的样式
  :animation="250"  // 动画时间
  :scroll="true"   // 是否可拖拽
  @add='handleAddPutList'  // 列表新增数据事件
  @update='sortPutList'  // 列表数据更新事件
>
  <div v-for="(item, index) in putList"
      draggable="true"
      :key="index"
      class="put-list animated fadeIn"
      @mouseover="putListMouseover(item, index)"
      @mouseleave="putListMouseleave(item, index)"
      @click.prevent="putListClick(item, index)"
      :class="{'putList-active': showHoverBorder === index || showHoverOperation === index}"
      >
      <!-- {{item.name}} -->
      <Render :component-name="item.componentName"
              :props="item.props"></Render>
      <div v-if="showHoverOperation === index"
            class="put-list-copy"
            @click="componentCopy(item, index)"></div>
      <div v-if="showHoverOperation === index"
            v-popover:componentDeletePopover
            class="put-list-delete"
            @click="componentDelete(item, index)"></div>
  </div>
</draggable>
```