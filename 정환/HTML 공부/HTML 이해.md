## HTML 이란?:  hyper text markup language

- 웹 페이지를 만드는 언어
- hyper text = 링크라고도 부른다.
- markup language
- 확장자가 html ex) http://www.naver.com/

## HTML 문법

- 태그
- 속성
- 태그의 중첩
- 빈 태그
- 공백
- 주석

**태그란?**:  HTML은 태그들의 중첩이다.  태그는 HTML에서 가장 기본 되는 규칙이다. 무언가를 표시하기 위한 꼬리표, 이름표라는 의미를 가진다.

태그를 사용하는 방법: 태그 <,> 기호로 표현된 <,> 기호 사이에 이름이 들어간다. 

<h1>을 이용해 'hello, HTML'을 출력하는 코드 종료태그 앞에는 '/'기호가
붙는다.

```html
<h1> hello, HTML</h1>
```

**요소란?**: 내용을 포함한 태그 전체를 요소(Element)라고 한다.

## 속성(ATTRIBUTE): 이름과 값으로 이루어져 있다.

```html
<h1 id = "title">Hello,HTML</h1> // 속성값은 홑따옴표(')와 쌍따옴표(")로 감싸 표현한다.

<h1 id = "title" class = "main"> Hello, HTML</h1> // 태그에 여러 속성을 선언할 수 있다.
여러 속성을 선언할 때는 공으로 구분해서 사용한다.

	//속성 선언 순서는 태그에 영향을 미치지 않으며 class를 id보다 먼저 선언해도 된다.
```

**속성의 종류**: 모든 태그에 사용할 수 있는 글로벌 속성과 특정 태그에서만 사용할 수 있는 속성으로 구분된다. 위의 예시는 글로벌 속성이다.

## 태그 중첩(NESTING TAGS): 태그 안에 다른 태그를 선언할 수 있다.

중첩해서 사용시 중첩되는 태그는 부모태그를 벗어나서는 안된다.

```html
<h1>Hello, <i>HTML</h1></i> //잘못된 태그 선언

<h1>Hello, <i>HTML</i></h1> //올바른 태그 선언
```

## 빈 태그(EMPTY TAG): 내용이 없는 빈 태그

```html
<br>
<img src ="">
<input type="">
//빈 태그의 예시
```

내용만 비어있을 뿐 속성을 통해서 화면에 나타내거나 화면에 표시되지 않더라도 다른 용도로 사용되는 태그 ex) 브라우저가 직접 화면에 내용을 그려줘야 하는 경우

## HTML에서의 공백

기본적으로 HTML은 두 칸 이상의 공백을 모두 무시한다.

```html
<h1>Hello, HTML</h1>
<h1>Hello,     HTML</h1>
<h1>
    Hello,
    HTML
</h1>

// HTML은 두 칸 이상의 공백과 개행을 모두 무시하기 때문에 위 세가지 모두 같은 텍스트가
 화면에 나타나게 된다.
```

## 주석(COMMENT TAGS): 주석은 화면에 노출되지 않고 메모의 목적으로만 사용하는 것을 의미한다.

```html
<!-- 주석의 기호는 이렇게 사용하면된다! -->
```

## HTML 문서 구조(HTML DOCUMENTS):

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <title>HTML</title>
    </head>
    <body>
        <h1>Hello, HTML</h1>
    </body>
</html>
```

- 문서 타입 선언 후에는 <html>태그가 나와야 하고 자식으로는 <head>태그와 <body>태그가 있습니다. <html>태그의 lang 속성은 어떤 언어로 선언 되었는지를 나타낸다.
- <head>태그에 위치하는 태그들은 브라우저 화면에 표시되지 않는다.
- <meta>태그의 charset 속성은 문자의 인코딩 방식을 지정한다.
- <body>태그는 실제 브라우저 화면에 나타나는 내용이 들어간다.
