---
title: swiper插件使用
date: 2016-12-29 14:04:02
tags: '插件'
description: Swiper 是一款免费以及轻量级的移动设备触控滑块的js框架，使用硬件加速过渡（如果该设备支持的话）。主要使用于移动端的网站、移动web apps，native apps和hybrid apps。主要是为IOS而设计的，同时，在Android、WP8系统也有着良好的用户体验，Swiper从3.0开始不再全面支持PC端。因此，如需在PC上兼容更多的浏览器，可以选择Swiper2.x（甚至支持IE7）。
photos: /images/swiper.png
---

## 资源
中文官网： [http://www.swiper.com.cn/](http://www.swiper.com.cn/)
Open CDN:     
```
//cdn.bootcss.com/Swiper/3.4.1/css/swiper.min.css
//cdn.bootcss.com/Swiper/3.4.1/js/swiper.min.js
//cdn.bootcss.com/Swiper/3.4.1/js/swiper.jquery.min.js
```
## 常用方法
```javascript
初始位置：          initialSlide: 0
垂直方向：          direction: 'vertical'
多个slide：         slidesPerView: 3
键盘控制：          keyboardControl: true
鼠标控制：          mousewheelControl: true
按钮控制：          paginationClickable: true
切换效果：          effect: 'fade'、'flip'、'cube'、'coverflow'
前后箭头：          swiper-button-black、swiper-button-white
分页箭头：          swiper-pagination-black、swiper-pagination-white
slide之间的间隙：   spaceBetween: 10
分页按钮样式：      paginationType:'bullets'、'progress'
手抓光标：          grabCursor: true
```

## 基础样式
```html
<div class="swiper-container swiper-base">
    <div class="swiper-wrapper">
      <div class="swiper-slide">
        <img src="./img/342593.jpg" alt="demo" />
      </div>
      <div class="swiper-slide">
        <img src="./img/347233.jpg" alt="demo" />
      </div>
      <div class="swiper-slide">
        <img src="./img/350163.jpg" alt="demo" />
      </div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>

    <!-- 如果需要导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>

    <!-- 如果需要滚动条 -->
    <div class="swiper-scrollbar"></div>
  </div>
```
```javascript
function swiperBase(){
    new Swiper ('.swiper-base', {
      autoplay: 1000,
      loop: true,
      paginationClickable: true,
      pagination: '.swiper-pagination',

      nextButton: '.swiper-button-next',
      prevButton: '.swiper-button-prev',

      scrollbar: '.swiper-scrollbar',
    })
  };
```

## 垂直滚动
```html
<div class="swiper-container swiper-vertical">
  <div class="swiper-wrapper">
    <div class="swiper-slide">
      <img src="./img/342593.jpg" alt="demo" />
    </div>
    <div class="swiper-slide">
      <img src="./img/347233.jpg" alt="demo" />
    </div>
    <div class="swiper-slide">
      <img src="./img/350163.jpg" alt="demo" />
    </div>
  </div>
  <div class="swiper-pagination"></div>
</div>
```
```javascript
function swiperVertical(){
    new Swiper ('.swiper-vertical', {
      autoplay: 1000,
      loop: true,
      paginationClickable: true,
      direction: 'vertical',
      pagination: '.swiper-pagination',
    })
  };
```

## 多个slider
```html
<div class="swiper-container swiper-more">
  <div class="swiper-wrapper">
    <div class="swiper-slide">
      <img src="./img/342593.jpg" alt="demo" />
    </div>
    <div class="swiper-slide">
      <img src="./img/347233.jpg" alt="demo" />
    </div>
    <div class="swiper-slide">
      <img src="./img/350163.jpg" alt="demo" />
    </div>
    <div class="swiper-slide">
      <img src="./img/342593.jpg" alt="demo" />
    </div>
    <div class="swiper-slide">
      <img src="./img/421823.jpg" alt="demo" />
    </div>
  </div>
  <div class="swiper-pagination"></div>

  <div class="swiper-button-prev"></div>
  <div class="swiper-button-next"></div>
</div>
```
```javascript
function swiperMore(){
  new Swiper ('.swiper-more', {
    autoplay: 1000,
    loop: true,
    slidesPerView: 3,
    spaceBetween: 10,
    paginationClickable: true,
    pagination: '.swiper-pagination',
    nextButton: '.swiper-button-next',
    prevButton: '.swiper-button-prev',
  })
};
```

## 焦点图
```html
<div class="gallery-box">
  <div class="swiper-container gallery-top">
    <div class="swiper-wrapper">
      <div class="swiper-slide">
        <img src="./img/342593.jpg" alt="demo" />
      </div>
      <div class="swiper-slide">
        <img src="./img/347233.jpg" alt="demo" />
      </div>
      <div class="swiper-slide">
        <img src="./img/350163.jpg" alt="demo" />
      </div>
      <div class="swiper-slide">
        <img src="./img/342593.jpg" alt="demo" />
      </div>
      <div class="swiper-slide">
        <img src="./img/421823.jpg" alt="demo" />
      </div>
    </div>

    <div class="swiper-button-prev swiper-button-white"></div>
    <div class="swiper-button-next swiper-button-white"></div>
  </div>
  <div class="swiper-container gallery-thumbs">
      <div class="swiper-wrapper">
          <div class="swiper-slide" style="background-image:url(./img/342593.jpg)"></div>
          <div class="swiper-slide" style="background-image:url(./img/347233.jpg)"></div>
          <div class="swiper-slide" style="background-image:url(./img/350163.jpg)"></div>
          <div class="swiper-slide" style="background-image:url(./img/342593.jpg)"></div>
          <div class="swiper-slide" style="background-image:url(./img/421823.jpg)"></div>
      </div>
  </div>
</div>
```
```javascript
function swiperMoreControl(){
   var galleryTop = new Swiper('.gallery-top', {
       initialSlide: 2,
       nextButton: '.swiper-button-next',
       prevButton: '.swiper-button-prev',
       effect: 'fade',
       spaceBetween: 10,
   });
   var galleryThumbs = new Swiper('.gallery-thumbs', {
       spaceBetween: 10,
       initialSlide: 2,
       centeredSlides: true,
       slidesPerView: 'auto',
       touchRatio: 0.1,
       slideToClickedSlide: true
   });
   galleryTop.params.control = galleryThumbs;
   galleryThumbs.params.control = galleryTop;
 };
```
```css
.gallery-top{height: 400px;}
.gallery-thumbs{height: 150px;padding: 10px;}

.gallery-box{background: #000;}
.gallery-thumbs .swiper-slide {background-size: cover;background-position: center;}
.gallery-thumbs .swiper-slide { width: 20%;height: 100%;cursor: pointer;}
```

## 延迟加载
```html
<div class="swiper-container swiper-img-lazy">
  <div class="swiper-wrapper">
    <div class="swiper-slide">
      <img class="swiper-lazy" src="./img/342593.jpg" alt="demo" />
      <div class="swiper-lazy-preloader swiper-lazy-preloader-white"></div>
    </div>
    <div class="swiper-slide">
      <img class="swiper-lazy" src="./img/347233.jpg" alt="demo" />
      <div class="swiper-lazy-preloader swiper-lazy-preloader-white"></div>
    </div>
    <div class="swiper-slide">
      <img class="swiper-lazy" src="./img/350163.jpg" alt="demo" />
      <div class="swiper-lazy-preloader swiper-lazy-preloader-white"></div>
    </div>
  </div>
  <div class="swiper-pagination swiper-pagination-white"></div>
</div>
```
```javascript
function swiperLazy(){
  new Swiper ('.swiper-img-lazy', {
    // autoplay: 1000,
    // loop: true,
    paginationClickable: true,
    pagination: '.swiper-pagination',
    preloadImages: false,
    lazyLoading: true
  })
};
```
