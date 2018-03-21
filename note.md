---
title: 日常笔记
date: 2017-10-26 16:25:00
tags: [文章,笔记]
---
日常笔记记录，有啥好玩的都要记录下来，好记性不如烂笔头，何况记性不好咧~
<!-- more -->
**1、类型判断**

        _.type = function (obj) {
            //直接会return一个字符串  "[objec 你传进了的数据的类型String/Number/Array/Object/Null/Undefined]"
            //然后正则匹配得到想要的类型
            return Object.prototype.toString.call(obj).replace(/\[object\s|\]/g, '');
        }

**2、table-layout**

  由于表格单元格的宽度根据其内容进行调整，设置了表格的宽度，但是不起作用，因为表格有个叫做table-layout的属性，其浏览器默认值是auto。
  当我们把这个值设置为fixed的时候，给th/td标签设置的宽度就起作用了。
   [\[ 相关文档链接 \]][1]

**3、CSS3 object-position/object-fit**
  对img等替换元素的处理~
  [\[ 相关文档链接 \]][2]

**4、CSS文字两端对齐**

        elem {  text-align: justify;  }
        elem:after { content: " "; display: inline-block; width: 100%;  }


**5、常用小函数**

        //随机颜色
        function getColor(){
        return '#' + (~~(Math.random() * 0xffffff)).toString(16).padStart(6,'0');
        }
        //区间随机数
        function rand(min, max) {
        return Math.random() * (max - min) + min;
        }


**6、数组深浅复制**

        [].concat(arr);
        Object.concat(toArr,formArr);


**7、html之marquee详解**

  活动字幕滚动标签，实测挺好玩的，就是在有限滚动次数结束时直接停在边界不是很好。
  [\[ 相关文档链接 \]][3]

**8、csp(conent-security-policy)**

  禁止来自外部脚本资源的引入
  [\[ 相关文档链接 \]][4]


  [1]: http://www.w3school.com.cn/cssref/pr_tab_table-layout.asp
  [2]: http://www.zhangxinxu.com/wordpress/2015/03/css3-object-position-object-fit/
  [3]: http://www.cnblogs.com/tuyile006/archive/2007/03/28/691329.html
  [4]: http://www.qdfuns.com/notes/26042/83538ff174859ffddc12ade1618336d2.html
