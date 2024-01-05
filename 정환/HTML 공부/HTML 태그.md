- HTML 버전이 업그레이드 되면서 태그가 새로 추가되기도 삭제되기도 한다.
- 실제로 대다수의 웹 페이지는 대략 25개 정도의 태그가 사용된다.
- html, head, body, title등 기본적으로 들어가는 태그들도 다 포함이 된다.

## 제목(HEADING) 태그: h1 ~ h6 문서내 제목을 표현할때 사용

```html
<!doctype html>
<html lang="ko">
    <head>
        <meta charset="utf-8">
        <title>heading tags</title>

    </head>
      <body>
      <h1>역사</h1>
      <h2>개발</h2>
      <p>안녕 나이거 개발함 역사 개쩜</p>

      <h2>최초 규격</h2>
      우리 규격 이랬음!
      </body>
</html>
```

## 단락 태그:단락이나 개행을 구분할때 사용

- **<p>**를 사용해서 단락으로 구분하면 자연스럽게 개행이 된다.
- **<br>**은 개행을 위해 쓰이는 태그이다. 닫기 태그와 내용이 존재하지 않는 빈 태그이다.

## 택스트를 표현하는 태그

- **<b>**: bold 태그는 글자를 굵게 표현하는 태그이다.
- **<i>**: italic 태그는 글자를 기울여서 표현하는 태그이다.
- **<u>**: underline 태그는 글자의 밑줄을 표현하는 태그이다.
- **<s>**: strike 태그는 글자의 중간을 표현하는 태그이다.

## 앵커(ANCHOR): 다른 문서로 이동할 수 있는 링크를 생성한다.

- href: 링크의 목적지가 되는 URL을 지정한다.
- **<a>**:(anchor 태그)는 a태그, 앵커, 링크등 여러 이름으로 불린다.

```html
<a href = "http://www.naver.com/"target="_blank">네이버</a>
```

### href 속성

링크를 만들기 위해 <a>는 반드시 href속성을 가지고 있어야 한다.

herf 속성의 값은 링크의 목적지가 되는 URL입니다.

### target 속성

traget 속성은 링크된 리소스를 어디에 표시할지 나타내는 속성이다. 속성값으로 _self, _blank, _parent, _top이 있다.

- _self는 현재 화면에 표시한다는 의미로, target 속성이 선언되지 않으면 기본적으로 self와 같이 동작한다.
- _blank는 새로운 창에 표시 한다는 의미로 외부 페이지가 나타나게끔 하는 속성
- _parent와 _top은 프레임이라는 특정 조건에서만 동작하는 속성

## 의미없이 요소를 묶기 위한 태그(CONTAINER): 태그 자체에 아무 의미가 없으며, 단순히 요소들을 묶기 위해 사용되는 태그

```html
<div>
		<span>Loren</span> ipsum dolor sit.
</div>
```

별다른 의미없이 다른 목적으로 필요할 때 사용한다. 

- **<div>**: block-level: 블록 레벨 태그입니다. <p>
- **<span>**: inline-level: 인라인 레벨 태그이다. <b>, <i> , <u> , <s>

## 리스트(list)

- **<ul>:** ul태그는 순서가 없는 리스트를 표현할 때 사용한다. 점으로 단락을 나눔
- **<ol>**: ol태그는 순서가 있는 리스트를 표현할 때 사용한다. 숫자로 단락을 나눔
- **<dl>**: dl태그는 용어와 그에 대한 정의를 표현할 때 사용한다.
- **<dt>**: 용어를 나타내는 태그
- **<dd>**:용어의 대한 정의 또는 설명을 나타내는 태그

```html
<!doctype html>
<html lang="ko">
    <head>
        <meta charset="utf-8">
        <title>heading tags</title>

    </head>
      <body>
      <h1>월드컵 조 편성</h1>
        <ol>
          <li>
            A조
            </li>
            <ul>
          <li>러시아</li>
          <li>우루과이</li>
          <li>이집트</li>
          <li>사우디아라비아</li>
        </ul>
      </body>
</html>
```

## 이미지(IMAGE): 문서에 이미지를 삽입하는 태그로, 닫는 태그가 없는 빈 태그 이다.

- 문서에 이미지를 삽입한다
- src: <img>의 필수 속성으로 이미지 경로를 지정한다.
- alt: 이미지의 대체 텍스트를 입력한다. (설명)
- width/height: 이미지의 가로,세 크기를 조정한다.

## 이미지 파일 형식

- gif: 제한적인 색을 사용하고 용량이 적으며 투명 이미지와 에니메이션 이미지를 지원
- jpg: 사진이나 일반적인 그림에 쓰이며 높은 압축률과 자연스러운 색상 표현을 지원하는 형식(투명을 지원하지 않는다.
- png: 이미지 손실이 적으며 투명과 반투명 모두 지원하는 형

## 표(table): 데이터 표를 나타내는 태그

- **<table>**: 표를 나타내는 태그
- **<tr>**: 행을 나타내는 태그
- **<th>**: 제목 셀을 나타내는 태그
- **<td>**: 셀을 나타내는 태그

하나의 <talbe>은 하나 이상의 <tr>로 이루어저 있다. <tr>은 셀을 나타내는 <th>,<td>를 자식으로 가지게 된다. 표를 구성할때는 위에서 밑으로 좌측에서 우측으로 작성하면 된다.

- **<caption>**: 표의 제목을 나타내는 태그
- **<thead>**: 제목 행을 그룹화하는 태그
- **<tfoot>**: 바닥 행을 그룹화하는 태그
- **<tbody>**: 본문 행을 그룹화하는 태그
- **<colspan>**: 셀을 가로방향으로 병합
- **<rowspan>**: 셀을 세로방향으로 병합

```html
<table>

    <caption>Monthly Savings</caption>
    <thead>
        <tr>
            <th>Month</th>
            
<th>Savings</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            
<td>January</td>
            <td>$100</td>
        </tr>
        <tr>
            
<td>February</td>
            <td>$80</td>
        </tr>

    </tbody>
    <tfoot>
        <tr>
            
<td>Sum</td>
            <td>$180</td>
        </tr>
    </tfoot>

</table>
```
