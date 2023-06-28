# hello
- 선택한 다음에 태그로 감싸주기 :: 익스텐션 htmltagwrap Alt + W

- css 선택자 사이에 빈줄 없애기 : 페이지 복붙..비효율적
- map(false), Vendor Prefixes(null) 생성 안하는법

- @at-root 선택자는 부모요소를 참조하지 않는다. 
ex)
<code>@at-root .heading{width:100px;}</code>
- 겹치는 접두사가 있으면 네스팅처럼 활용 가능
ex) 
<code>
    font: {
            family: 'Raleway', sans-serif;
            size: 18px;
            weight: bold; 
        }
</code>
- :is() 가상클래스
ex) 
<code>
    :is(header, section, footer) h1{
        font-size:30px;
    }
</code>

- Variables
네이밍은 제목+색상
<code>
    $heading-color
    $heading-fc
    $heading-bgc
</code>
변수는 '',""로 묶지 않는다. 
<code>
background-image: url($portfolio-images-url + "blog-post-01.jpg");
</code>

css에서 변수 선언하는 방법
<code>
    :root{
        --변수명: 값;
    }
    .text{
        color: var(--변수명);
    }
</code>


- @import "파일명";
<code>
    @import "reset";
    @import "reset.css";
</code>

- 산술연산자
변수나, 그냥 선언하며 +-*/% 사용 가능.

- 재사용 선언과 사용
<code>
    @mixin{
    
    }
    @include{
        
    }
</code>

인수를 사용할 경우

<code>
    @mixin button-padding($updown, $leftright){
      padding: $updown $leftright;
    }
    .yes{
     @include button-padding(5px, 10px);
    }
</code>


- 따로 파일을 만들어야 하는 scss
_font.scss
_reset.scss
_variables.scss
_mixin.scss


- extend
다른 css 선언된 속성을 가져와서 쓸 수있다.
기존에 있는 css를 심플하게 가져다 쓸 때 사용한다.
더 확장성있게 사용하려면 mixin - include를 쓴다

<code>
    .shape{
        border:1px solid #000;
        width:250px;
        height:300px;
        border-radius: 5px;
        box-shadow: 0 0 5px 10px rgba(0, 0, 0, 0.2);
    }
    .card{
        &-item{
            @extend .shape;
        }
    }
</code>

- %(플레이스홀드 선택자)
shape라는 선택자는 없어지고,
컴파일된 파일에서는 extend 불러오는 선택자로 새로 정의된다.
html에서 해당 선택자가 없고, css에서만 쓸 때 %를 쓴다.
컴파일되면 %로 선언된 선택자는 없다.
사용된 것만 컴파일된다.

%shape = .card-item 으로 컴파일됨.

<cods>
    
    %shape{
        border:1px solid #000;
        width:250px;
        height:300px;
        border-radius: 5px;
        box-shadow: 0 0 5px 10px rgba(0, 0, 0, 0.2);
    }
    .card{
        &-item{
            @extend %shape;
        }
    }
</cods>

- 다중 변수 map-get()
<code>
    color나 font-family, font-size 정의해놓고 쓰면 편함
    
    $color:(
      font-primary: #2d3456,
      font-secondary: #636e72,
      font-focus: #0984e3,
      bgc-primary: #eee,
      bgc-secondary: #b2bec3
    );
    
        $font-family: (
          kor: "'Noto Sans KR', sans-serif",
          eng: "'Raleway', sans-serif"
        )
        
        body{
            background-color: map-get($color, bgc-primary);
             font-family: map-get($font-family, eng);
        }
</code>

- 기본 텍스트 서식 설정 (셀프 자동화)
이중 중첩 믹스인, 접두어 선언을 통해 간결화 

<code>
@mixin font-default{
  font: {
    size: $font-base;
    weight: normal;
    family: $font-family-base, sans-serif;
  }
  line-height: normal;
}

@mixin font-medium{
  @include font-default;
  font-size: $font-base * 2;
}

@mixin font-large{
  @include font-default;
  font-size: $font-base * 3;
}
</code>

- @mixnin 배열에 매개변수 -> @include 인수 반환

<code>
.text-link{
    @include links(black, gold, yellow, crimson);
}

@mixin links($link, $visited, $active, $hover){
    text-decoration: none;
    color:$link;
      &:visited{
          color:$visited;
      }
      &:active{
          color:$active;
      }
      &:hover{
          color:$hover;
      }
}
</code>

- 단위를 하나 정해서 변할수도 있는 속성에 모두 넣어 나눈다.
ex)
<code>
$icon-box-size:100px;
box-shadow: 
          0 0 ($icon-box-size / 10) rgba(116, 186, 255, 0.5),
          0 0 ($icon-box-size / 6.66) rgba(116, 186, 255, 0.5),
          0 0 ($icon-box-size / 5) rgba(116, 186, 255, 0.5),
          inset 0 0 ($icon-box-size / 33.33) rgba(116, 186, 255, 0.5);
          text-shadow: 
          0 0 ($icon-box-size / 10) #74b9ff,
          0 0 ($icon-box-size / 6.66) #74b9ff,
          0 0 ($icon-box-size / 5) #74b9ff;


width: $icon-box-size;
height: $icon-box-size;
border: $icon-box-size / 33.33 solid #fff;
border-radius: $icon-box-size / 10;
background-color: #111;
font-size: $icon-box-size / 2;
</code>

-  자주 쓰는 색을 변수로 정해서 sass function을 쓴다.
sass function
sass-lang.com/documentation/modules/map
color:opacify($color,0.3)
transparentize($color,0.5)
<code>
$icon-color: #74b9ff;
box-shadow: 
          0 0 ($icon-box-size / 10) transparentize($icon-color, 0.5),
          0 0 ($icon-box-size / 6.66) transparentize($icon-color, 0.5),
          0 0 ($icon-box-size / 5) transparentize($icon-color, 0.5),
          inset 0 0 ($icon-box-size / 33.33) $icon-color;
          text-shadow: 
          0 0 ($icon-box-size / 10) $icon-color,
          0 0 ($icon-box-size / 6.66) $icon-color,
          0 0 ($icon-box-size / 5) $icon-color;

</code>