# less

> less 是动态的样式表语言，通过简洁明了的语法定义，使编写 CSS 的工作变得非常简单。

*注意：其他未提及的东西请参照css*

### 顺序

> 书写的顺序按照 属性、伪类、继承选择器 排序，并且三者之间都要有空行分隔。

按照上述的顺序，代码看起来会简洁很多。如：

```
.bg-banner {
  background: #333;

  &:hover {
    color: #eee;
  }

  .bg-banner-title {
    font-size: 20px;
  }
  .bg-banner-desc {
    font-size: 16px;
  }
}
```

### 模块化

> 模块化：每个独立的div。

有时候会遇到这样的情况，对于页面中重复的list表单，可以对每个item进行模块化。
```
<div class="bg-post">
  <p class="bg-title">自你往天猫宝里存钱，你的手已剁</p>
  <span class="bg-desc">.......</span>
</div>
```
如上代码，可能会出现类`.bg-title`出现在其他地方，除非bg-title显示的样式一样，不然为了避免冲突，应该命名如下：
```
<div class="bg-post">
  <p class="bg-post-title">自你往天猫宝里存钱，你的手已剁</p>
  <span class="bg-post-desc">.......</span>
</div>
```

> 模块嵌套：大模块可有子模块命名。

```
<div class="bg-post">
  <p class="bg-post-title">自你往天猫宝里存钱，你的手已剁</p>
  <div class="bg-meta">
    <span class="bg-meta-desc">....</span>
    <div class="bg-desc">
      <img class="bg-desc-img">
    </div>
  </div>
</div>
```
这样的选择器可以这样写: `.bg-post > bg-desc .bg-desc-img`


