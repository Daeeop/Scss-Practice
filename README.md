# SCSS 

```plaintext
index.html 파일에 scss 파일은 연결 하면 Parcel-bundler 패키지를 통해서  
분석되서 실제 브라우져 에서는 css로 변환되서 동작 하는 개념
```

# 주석 처리 방법

```plaintext
/* color : red; */   
// color : red;  
// 방식은 css로 변환 했을때 화면에 나타나지 않는다.
```

# SCSS 중첩 기능

```html
 <div class="container">
   <ul>
     <li>
       <div class="name">Daeeop</div>
       <div class="age">28</div>
     </li>
   </ul>
  </div>
```
이러한 HTML 코드가 존재 할 때 SCSS 에서는 이렇게 적용 할 수 있다.

```css
.container {
  ul {
    list-style: none;
    li {
      font-size: 40px;
      .name {
        color: royalblue;
      }
      .age {
        color: orange;
      }
    }
  }
}
```
위의 HTML 코드를 CSS 문법으로 적용 하면 다음과 같다.

```css
.container ul  {
  list-style: none;
}

.container ul li {
  font-size: 40px
}

.container ul li .name {
  color: royalblue;
}

.container ul li .age {
  color: orange;
}
```

이렇게 css 문법에서는 `상위 선택자 .container`를 반복적으로 사용해야 하는데  
SCSS 에서는 그럴 필요가 없다!