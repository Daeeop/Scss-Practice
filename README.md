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

`SCSS 에서는 선택자를 중첩기능이 있고 속성 네임스페이스도 중첩 해주는 기능이 있다.`

```css
.box {
  font-weight: bold;
  font-family: sans-serif;
  margin-top: 10px;
  margin-bottom: 20px;
  padding-left: 20px;
  padding-right: 20px;
}
```
이러한 CSS 코드가 있을때 `font , margin , padding` 과 같은 NameSpace를 반복적으로 작성 하였다.

```css
.box {
    font :{
        weight : bold;
        family : sans-serif;
        
    };
    
    margin: {
        top: 10px;
        bottom : 20px;
    };
    
    padding: {
      left: 20px;
      right: 20px;
    };
}
```
SCSS 에서는 이런식으로 코드를 작성하여 속성에 NameSpace에 대해 중첩기능을 제공 한다.

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

이런식으로 위치,너비 같은 수치가 항상 똑같아야 할때는 그 수치를 변수로 만들어 사용하는게 편리하다.
```

### 변수 주의사항
<br>

```plaintext

1. 변수는 선언된 범위 내에서 유효 범위를 가진다. (자바스크립트 let , const와 같은 개념)

2. 선언된 변수에 값을 재 할당 가능하다. (유효범위 주의)

2.1 전역변수로 변수를 선언 하고 재할당을 중괄호 안에서 했으면 그 중괄호가 재할당된 값의 유효 범위 (나머지는 기존 값)

```

# 산술 연산 

`SCSS 에서는 산술 연산자 (+ , - , * , / , %) 이용 가능`

```css

div {

    $number : 20px;
    width: 20px + 20px;
    height: 40px - 10px;
    font-size: 10px * 2;
    // 나누기 연산자 이용하는 방법
    margin: (40px / 2);
    bottom: $number / 2;
    top: (16px + 12px) / 3;
    padding: 20px % 3;

}

나누기 연산자는 표준 CSS 에서 font속성의 단축 속성으로 슬러쉬 기호로 구분하는 문법이 있다.
그렇기 때문에 일반적으로 동작 하지 않기 때문에 괄호로 묶거나 , 수치를 변수에 할당 하거나 , 다른 연산자와 함께 사용 해야 한다.

```

```css
div {

  width: 40px;
  height: 30px;
  font-size: 20px;
  margin: 20px;
  bottom: 10px;
  top: 9.3333333333px;
  padding: 2px;

}

< 주의사항 >

  산술 연산은 같은 단위 끼리만 가능 

  width: 100% - 200px; // 불가


```

# 재활용(Mixins)

`SCSS 에서는 여러가지 속성을 Mixin 이라는 어노테이션을 이용해 재활용 하여 사용 할 수 있다.`

``` html
<div class="container">
   <div class="item">
     Mixin!
  </div>
</div>  
```
```css
.container {

  width: 200px;
  height: 200px;
  background-color: orange;
  display: flex;
  justify-content: center;
  align-items: center;

}

.container .item {

  width: 100px;
  height: 100px;
  background-color: royalblue;
  display: flex;
  justify-content: center;
  align-items: center;

}

컨테이너 클래스 선택자와 그 자식인 아이템 클래스 선택자에 공통으로 들어가는 속성이 있다.
  display: flex;
  justify-content: center;
  align-items: center;
```

SCSS 에서는 공통으로 쓰이는 속성에 대해서 Mixin 이라는 기능을 제공 한다.

```css
@mixin center {
    display: flex;
    justify-content: center;
    align-items: center;
}

이렇게 정의를 해두고 사용 할때는 @include 어노테이션을 붙여서 사용 할 수 있다.

.container {
    @include center;
    .item {
        @include center;
    }
}

위의 코드를 CSS로 변환 하면 아래에 코드 이다.

.container {

  display: flex;
  justify-content: center;
  align-items: center;

}

.container .item {

  display: flex;
  justify-content: center;
  align-items: center;

}
```

근데 만약 재활용 하여 사용하려는 속성의 값을 바꾸고 싶은 경우가 생길 수도 있는데  
자바스크립트의 함수의 매개변수 처럼 SCSS 에서도 매개변수를 사용 할 수 있다.

```css
@mixin center($position) {
    display: flex;
    justify-content: $position;
    align-items: $position;
}

이렇게 매개변수를 이용하면 속성을 재활용 하되 그 안에 값은 우리가 마음대로 지정 할 수 있다.

.container {
    @include center(flex-end);
    .item {
        @include center(center);
    }
}

위의 코드를 CSS 문법으로 변환 하면 

.container {

  display: flex;
  justify-content: flex-end;
  align-items: flex-end;

}

.container .item {

  display: flex;
  justify-content: center;
  align-items: center;

}

하지만, 이런식으로 Mixin 을 사용하게 되면 우리가 처음에 설정한 기본값이 사라지는데  
SCSS 에서는 기본값을 설정 할 수 있게 제공 하고 있다.

@mixin center($position: center) {
    display: flex;
    justify-content: $position;
    align-items: $position;
}

.container {
    @include center(flex-end);
    .item {
        @include center;
    }
}

이렇게 인수를 명시 하지 않으면 알아서 기본값으로 인식 한다.
```

```scss
또 자바스크립트의 함수와 동일하게 쉼표로 구분하여 여러가지의 매개변수를 입력 할 수 있다.

@mixin center($position : center , $color : red) {

    display: flex;
    justify-content: $position;
    align-items: $position;
    background-color : $color;

}

.container {
    @include center(flex-end);
    .item {
        @include center;
    }
}

위의 코드를 CSS로 변환 하면

.container {

  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  background-color: red;

}

.container .item {

  display: flex;
  justify-content: center;
  align-items: center;
  background-color: red;

}

인수로 $color에 대한 색상을 명시하지 않았기 때문에 기본값으로 지정된 red가 들어가 있다.

.container {
  @include center(blue)
}

만약 위의 코드 처럼 위치에 대한 값은 기본값 색상에 대한 값은 우리가 원하는 값을 넣고 싶을때
위의 코드는 justify-content , align-items 속성에 대한 값으로 blue가 들어가 오류를 발생 시킨다.
인수를 넣을때도 매개변수에 순서대로 인수를 넣어야 한다.

이럴 경우에 2가지 방법이 있는데

1. @include center(center , blue) 처럼 기본값을 명시 해주는 방법

2. @include center($color : blue) 처럼 키워드 인수를 사용 하는 방법이 있다.
 
```

# 반복문

`SCSS 에서도 자바스크립트 처럼 반복문을 사용 할 수 있다.`

```javascript
자바스크립트 반복문

for(let i = 0; i < 5; i++) {
  console.log(`${i} 번째 입니다.`);
}

SCSS 반복문 

@for $i from 1 through 3 {
    .box:nth-child(#{$i}) {
        width: 100px * $i; 
  }
}

위의 코드를 CSS로 변환하면 아래의 코드가 실행 된다.

.box:nth-child(1) {
  width: 100px;
}

.box:nth-child(2) {
  width: 200px;
}

.box:nth-child(3) {
  width: 300px;
}

```

# 함수

`SCSS 에서 @function 키워드를 이용하여 함수를 사용 할 수 있다.`

```css
@function height($size , $ratio) {
  @return $size * $ratio
}

.box {

  $width: 100px;
  width: $width;
  height: height($width , 1/2);

}

.box {

  width: 100px;
  height: 50px; // height 함수를 통해서 값 설정

}

```

# 색상 내장함수

``` css
1. mix(red , black); // red + black 조합한 색상을 반환 한다.

2. lighten(red , 10%); // red 컬러를 10% 밝게 만든다.

3. darken(red , 10%); // red 컬러를 10% 어둡게 만든다.

4. saturate(red , 10%); // red 컬러 채도를 10% 높여 준다.

5. desaturate(red , 10%); // red 컬러의 채도를 10% 채도를 낮춰 준다.

6. grayscale(red); // 회색으로 만든다..?

7. invert(red); // red 컬러 색상을 반전 시킨다.. 

8. rgba(red , .5); // red 컬러에 50% 투명도 추가

8-1 표준 CSS : rgba(0,0,0,.5) 

```

# 다른 SCSS 파일 가져오기

```scss
1. @import url("파일.scss");

2. @import "파일.scss";

3. @import "파일"; 

4. @import "파일" , "파일2";
```