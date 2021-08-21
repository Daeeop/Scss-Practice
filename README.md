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

이렇게 css 문법에서는 `상위 선택자 .container`를 반복적으로 사용해야 하는데 SCSS 에서는 그럴 필요가 없다!  


```plaintext
후손 요소가 아닌 자식 요소로 인식을 하고 싶으면 '>' 를 추가 해주면 된다.
```

# 상위 선택자 참조(&) , 자신이 속한 범위에 있는 상위 선택자 참조

```css

.btn {
  position: absolute;
}
.btn.active {
  color: red;
}
```
이러한 CSS 코드를 SCSS 문법으로 바꿔보면

```css

.btn {
    position: absolute;
    &.active {
        color: red;
    }
}
```

이렇게 사용 할 수 있다.  
btn 이라는 클래스를 가지고 있고 일치선택자로 .active클래스가 가진 HTML요소가 있을때  
SCSS 에서는 & 기호를 사용하여 중첩 기능을 그대로 사용 할 수 있다.  
`& : .btn `이다.  **&이 .btn으로 치환 된다.**

<br>

```css

.fs-small {
  font-size: 14px;
}
.fs-medium {
  font-size: 16px;
}
.fs-large {
  font-size: 18px;
}
```
```css

.fs {
    &-small { font-size : 14px};
    &-medium { font-size : 16px};
    &-large { font-size : 18px};
}
```

상위 선택자가 `&` 가 있는 부분에 치환되어 들어간다 라고 생각 해도 된다.
<br>

# 중첩된 속성

# 변수(Variable)

`SCSS 문법에서는 CSS 와는 다르게 속성을 변수에 담아 둘 수 있다.`

```css
.container {
    position: fixed;
    top: 100px;
    
    .item {
        width: 100px;
        height: 100px;
        transform: translateX(100px);
    }
}
```

이러한 SCSS 코드가 있을때 반복되는 100px 이라는 수치에 대해서 변수로 담아 둘 수 있다.

```css
$size : 100px;

.container {
    position: fixed;
    top: $size;
    
    .item {
        width: $size;
        height: $size;
        transform: translateX($size);
    }
}

이런식으로 위치 ,너비 같은 수치가 항상 똑같아야 할때는 그 수치를 변수로 만들어 사용하는게 편리하다.
```

### 변수 주의사항
<br>

```plaintext

1. 변수는 선언된 범위 내에서 유효 범위를 가진다. (자바스크립트 let , const와 같은 개념)

2. 선언된 변수에 값을 재 할당 가능하다. (유효범위 주의)

2.1 전역변수로 변수를 선언 하고 재할당을 중괄호 안에서 했으면 그 중괄호가 재할당된 값의 유효 범위 (나머지는 기존 값)


```
