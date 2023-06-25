# hello
- 선택한 다음에 태그로 감싸주기 :: 익스텐션 htmltagwrap Alt + W

- css 선택자 사이에 빈줄 없애기 : 페이지 복붙..비효율적
- map(false), Vendor Prefixes(null) 생성 안하는법

- @at-root 선택자는 부모요소를 참조하지 않는다. 
ex) @at-root .heading{width:100px;}
- 겹치는 접두사가 있으면 네스팅처럼 활용 가능
ex) 
font: {
        family: 'Raleway', sans-serif;
        size: 18px;
        weight: bold; 
    }
- :is() 가상클래스
ex) 
:is(header, section, footer) h1{
    font-size:30px;
}

- Variables
네이밍은 제목+색상
$heading-color
$heading-fc
$heading-bgc
변수는 '',""로 묶지 않는다. 
background-image: url($portfolio-images-url + "blog-post-01.jpg");

css에서 변수 선언하는 방법
:root{
    --변수명: 값;
}
.text{
    color: var(--변수명);
}
