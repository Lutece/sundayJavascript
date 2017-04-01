#Sass

##Sass에 대해

Sass의 궁극적인 목적은 CSS의 결함을 보정하는 것에 있다.

<pre>
공식문서 : Sass는 기초 언어에 힘과 우아함을 더해주는 CSS의 확장이다.
</pre>

###Sass란 무엇인가?
Sass는 CSS 전처리기이다.
우리가 작성하는 스카일시트와 브라우저에서 해설할 .css 파일 중간에 위치하는 하나의 계층이다.

Sass(Syntactically Awesome Stylesheets)는 하나의 언어로서 CSS의 구멍들을 메워주고, DRY 방식을 적용해서 더 빠르고 효율적으로 코드를 작성하고 쉽게 유지보수할 수 있도록 도와준다.

###Preprocessing

Sass로 시작하면 처리 된 Sass 파일을 웹 사이트에서 사용할 수 있는 일반 CSS파일로 변환해줘야 한다.

변환 : 개별 파일 또는 전체 디렉토리 보면서 Sass를 실해아 할 수 있다.

<pre>
sass --watch app/sass:public/stylesheets
</pre>

###Variables

변수를 만들어 자바스크립트에서 사용 하듯이 지정하여 재사용 할 수 있다.

<pre>
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
</pre>

###Nesting

HTML의 동일한 시각적 계층 구조를 따르는 방식 (부모 형제)

<pre>
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
</pre>

###Partials
다른 Sass 파일에 포함 할 수있는 CSS 스 니펫을 포함하는 부분 Sass 파일을 만들 수 있습니다. 이것은 CSS를 모듈화하고 유지 관리를 쉽게하는 데 도움이됩니다. 부분은 단순히 밑줄로 시작하는 Sass 파일입니다. 너는 그것과 비슷한 이름을 지을지도 모른다 _partial.scss. 밑줄은 Sass가 파일이 부분 파일 일 뿐이며 CSS 파일로 생성되어서는 안됨을 알립니다. Sass 부분은 @import지시문 과 함께 사용됩니다 .
