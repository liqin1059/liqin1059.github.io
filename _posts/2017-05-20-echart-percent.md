---
layout: post
title: echart设置百分比数据
date: 2017-04-14 12:31:30
categories: echart
tags: [大数据]
---
设置echart数据中有时会用到百分比数据需要进行配置转换
## 设置百分比数据
在series中：
```
{
    name:'我的店',
    type:'bar',
     itemStyle: {
        normal: {
            color: '#00cc99',
            barBorderRadius:0,
            label : {
                show: true,
                position: 'top',
                textStyle:{
                      color:'#3b3b3b'
                },
                formatter:'{c} %'
            }
        }
    },
    data:myStoreIncomeData
}
```
> 使用formatter设置

## 设置两个bar之间的距离
使用series中的barGap
```
{
    name:'同行的店',
    type:'bar',
    itemStyle: {
        normal: {
            color: '#fff3c9',
            barBorderRadius:0,
            label : {
                show: true,
                position: 'top',
                textStyle:{
                      color:'#3b3b3b'
                }
            }
        }
    },
    data:StoresData,
    barGap:'0.1%'
}
```







