## Web Crawling

####BeautifulSoup 을 활용하여 간단한 웹 크롤러를 만드는 방법입니다. 

---

```sh
# 필요한 패키지 임포트 - 터미널에 해주세요
pip install requests
pip install html5lib  # parser 에 따라 다름
pip install BeautifulSoup
```
**1. 사이트(웹 서버)로의 요청(request) 보내기**

사이트(웹 서버)로의 요청(request)의 종류

1) get 방식 (기본값) 과정
사이트/서버 에 url을 통해 '검색어 "머신러닝"을 검색하겠다'는 요청을 보냅니다. -> 검색어가 url 주소와 함께 서버로 같이 전송됩니다. -> 서버에서 응답된 결과를 변수에 저장하고, 리턴합니다.

cf. url 의 구조
https://search.___.net(사이트 이름)/(서버이름)search?w=tot(컴퓨터에서 서버로 전송되는 정보의 단위1) & q=%EC%A0%95%EA%B2%BD%EC%A7%84&DA(정보의 단위2) =NTB
- / 부터 & 까지가 정보의 단위 하나입니다.



2) post 방식
(ex 로그인) 정보를 감춰서 요청을 보낸다.

이 포스트에서는 get 방식(기본값)을 사용하였습니다.

```python
# 접속할 사이트(웹 서버) 주소
url = 'https://search.daum.net/search?w=news&q=%EB%A8%B8%EC%8B%A0%20%EB%9F%AC%EB%8B%9D&DA=YZR&spacing=0'
# 사이트(웹 서버)로 요청(request)을 보냄
html = requests.get(url).text.strip()
# 요청의 결과(응답 response)을 html 이라는 변수에 저장
# .text.strip() - text 만 보이게 / strip() 앞뒤 공백 뺌
```

---

**2. 파서(Parser)를 사용하여 파싱하기**

파싱(Parsing, 구문분석) 이란, 컴퓨터 과학에서 파싱((syntactic) parsing)은 일련의 문자열을 의미있는 토큰(token)으로 분해하고 이들로 이루어진 파스 트리(parse tree)를 만드는 과정을 말합니다. (https://ko.wikipedia.org/wiki/%EA%B5%AC%EB%AC%B8_%EB%B6%84%EC%84%9D 참조)   
말이 조금 어렵게 들리는데, 저는 어떠한 데이터를 문법적으로 해부해서 (Parse 의 뜻) 다른 형태의 데이터로 만들어주는 것으로 이해했습니다. 이렇게요.

![파서](data:image/png;base64,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)
[파싱-위키백과](https://images.app.goo.gl/VYHWLyodd1G37gJ76) 참조

그리고 이렇게 파싱을 해주는 프로세서라고 볼 수 있습니다.
BeautifulSoup 의 파서의 종류는 여러가지가 있습니다.
![Web%20Crawling/Untitled.png](./img/crawling.png) 
(https://brownbears.tistory.com/414 불곰님의 포스트에서 이미지를 가져왔습니다.)   
   
이 포스트에서는 html5lib 이라는 파서를 사용하겠습니다.   
   저장한 html이라는 변수로부터 BeautifulSoup 모듈을 이용하여 분석을 해놓은 상태를 soup라는 변수에 저장합니다.   

BeautifulSoup 모듈 : HTML 태그와 같은 컨텐츠들을 사용자들이 쉽게 파싱하기 쉽도록 도와주는 라이브러리
BeautifulSoup 모듈의 BeautifulSoup 메소드를 쓰는 방법은 다음과 같다.
```sh
Beautifulsoup(응답 or 문자열, parser의 종류)
```
```python
# HTML 문서와 HTML parser(분석기)를 파라미터에 전달해서, BeautifulSoup 객체 생성
soup = BeautifulSoup(html, 'html5lib')
```
---
**3. HTML 태그를 찾아서 출력하기**
   
HTML 태그의 종류는 HTML을 공부해야 알 수 있습니다.(ㅜㅜ) 그렇지만 HTML은 금방 익힐 수 있습니다. 
(https://heropy.blog/2019/05/26/html-elements/ 한눈에 보는 HTML 요소(Elements & Attributes) 총정리를 참고하시면 좋을 것 같습니다)

제가 정리한 HTML 구조는 다음과 같습니다. (틀릴 수도 있으니 양해 부탁드립니다)
```sh
    html의 구성 : tag/attribute/contents
    
    tag : html, body, h1, p, div, img,..
          start tag 와 end tag 가 짝을 이룬다 (error는 브라우저에서 보인다 - 코드 상으로는 보이지 않는다!)
          tag1 는 tag2 를 가질 수 있다(tag1 부모 요소, tag2 자식 요소 - 계층구조를 가진다)
          meta tag 같이 content 가 없는 tag 는 </> 로 start tag 에서 끝낼 수 있다
    
    attribute : start tag 안에서 속성들을 설정하기 위해서 사용
                charset, href, src, style,..
    
    content : start tag 와 end tag 사이의 내용들

    브라우저(Chrome, IE, Firefox, ..)는 HTML 문서를 분석해서 화면에 보여준다.
    즉, 태그로 이루어진 문서를 브라우저가 화면에 보여줄 수 있도록 렌더링한다

    <h1> .. <h6> : 제목 (큰..작) bold체
    <p> : 본문
    <div> : 브라우저 안에서 화면 영역을 나눠주는 용도. 브라우저의 구조를 잡는 역할
    <b> : bold체
    <a> : anchor, 화면에 링크를 만들어주는 역할

    box 모양 : 파란색 content / padding 안쪽여백 / border 테두리선 / margin 바깥여백 /
    줄바꿈은 옵션 (블록 레벨 태그 (줄바꿈 있음) <-> 인라인 태그 (줄바꿈 없음)) - 태그를 이용해서 넣지 않는 enter -> 화면에 반영되지 않는다.
    <br/> : 줄바꿈
    semantic tag : <strong></strong>처럼 의미가 들어간 태그 - html5에서 새로 추가된 태그 / 웹크롤러가 사용하는 태그 / 웹 검색 엔진에서 더 잘 검색됨
```
```sh
HTML 하위 요소(sub/child element)를 찾는 방법:
    1) parent_selector >(꺽쇠) child_selector : 바로 아랫쪽에 있는 element 를 찾아갈 수 있는 방법
    ex_ TAG : div > ul > li
    class, id 도 똑같이 쓸 수 있다.
    ex_ CLASS/ID : .coll_cont > #clusterResultUL > .fst
    문제점 : 너무 많이 써야 해서 a 로 가기 힘들다 (하나씩 밑으로 내려가니까)

    2) ancestor_selector(조상 선택자) descendant_selector(자손 선택자) : 자손들을 모두 찾아가겠다는 의미. 공백을 주면 된다.
    ex_ div li (div 의 자손 요소들 중에 li 들)
    ex_ .coll_cont .fst (클래스 .coll_cont 요소의 자손 요소들 중 클래스가 .fst 인 요소들)
```   
   
_HTML elements를 찾는 방법 1. find()_
```python
# find
# : for 문처럼 찾으면 바로 리턴 (처음부터 분석 하다가 가장 처음에 만나는 요소를 리턴)
print(soup.find('a'))  # a (anchor tag) 를 하나 밖에 찾을 수 없다.
print(soup.a)  # 같은 결과
```
_HTML elements를 찾는 방법 2. find_all()_
```python
# find_all
# : HTML 문서 전체에서 찾은 모든 해당 요소들의 리스트를 리턴함.
# soup('태그이름')과 같다.
print(soup.find_all('a'))
print(soup('a'))  # 같은 결과 : soup('태그이름')은 soup.find_all('태그이름')과 동일
print(soup('a')[0])  # 0 번째 인덱스 출력
```
_ex_HTML 요소들 중에서 tag 이름으로 h1, h2 요소 찾기_   
```python 
# (1) soup.find('태그이름')
h1 = soup.find('h1')
print(h1)  # element 를 찾았다!
print(h1.text)  # h1 element 안의 다른 html tag 들어가 있어서 - text 사용
# (2) soup.태그이름
h2 = soup.h2
print(h2)
print(h2.string)  # string 사용 - 문자열 찾아줌 (text 도 사용 가능)
```
_HTML 의 attribute 이름으로 태그를 찾는 방법 .get()_
```python
# .get('attribute_이름')
# : HTML 문서의 'a'라는 element 에서 attribute_이름을 가지고 있는 값을 구한다.
for link in soup('a'):
    # HTML_element.get('attr 이름') - attr 의 값을 구함. 
    print(link.get('href'))  # href - 링크만 리턴
```
_ex_HTML 문서의 모든 링크에 걸려 있는 주소들을 출력하기_

```python
soup = BeautifulSoup(html, 'html5lib') # html5lib 파서 사용
for link in soup('a'):
    print(link.get('href'))  # href : 링크
```
_HTML class 로 태그를 찾는 방법_
```python
# class 로 요소를 찾는 방법 (1) (2)
# (1) Dictionary 로 찾기
# HTML 문서 안의 "class1" 클래스 속성을 갖는 모든 요소들을 찾음
for cls_1 in soup.find_all(attrs={'class':'class1'}):
    print(cls_1)
# class (attribute 이름) = "class1" (attribute 값)
# 클래스의 이름과 값을 dict 형태로 attrs= 속성에 넣어준다
# or
for cls_1 in soup(attrs={'class':'class1'}):
    print(cls_1)

# (2) class_ 라는 속성으로 찾기
# 속성으로 찾을 때에는
# (class는 이미 파이썬에서 사용하는 예약어이기 때문에 _를 붙였다)
# HTML 문서 안의 "class2" 클래스 속성을 갖는 모든 요소들을 찾음
for cls_2 in soup.find_all(class_='class2'):
    print(cls_2)
# or
for cls_2 in soup(class_='class2'):
    print(cls_2)
```

___
   
**4. 최종 : 웹페이지에서 스크롤링하기**
```python
# 접속할 사이트(웹 서버) 주소
url = 'https://search.daum.net/search?w=news&q=%EB%A8%B8%EC%8B%A0%20%EB%9F%AC%EB%8B%9D&DA=YZR&spacing=0'
# 사이트(웹 서버)로 요청(request)을 보냄
html = requests.get(url).text.strip()
# 요청의 결과(응답 response)을 html 이라는 변수에 저장
print(html[0:100])

# HTML 문서의 모든 링크에 걸려 있는 주소들을 출력
soup = BeautifulSoup(html, 'html5lib')
for link in soup('a'):
    print(link.get('href'))

# 개발자도구에서 코드에 더블클릭 - coll_cont 를 찾는다.
# class = "coll_cont" 는 사이트 내 여러개 있을 수 있으므로 확인해보자
# id 를 여러개 사용하는 경우도 있으므로, 장담할 수 없음
# 방법 1 : class 로 찾기 - 같은 클래스 이름이 있는 모든 HTML 요소들을 찾음
div_coll_cont = soup.find_all(class_='coll_cont')  # soup.find_all(attrs={'class': 'coll_cont'})
print(len(div_coll_cont))  # div_coll_cont 가 4 개가 나옴 - 개발자도구에서 우리가 찾는 coll_cont 가 몇번째인지 찾기 (ctrl+f) : 다른 부분들 찾기 (enter)

# soup.select(css_selector) : soup 객체에서 CSS 선택자로 요소들을 찾는 방법
news_link = soup.select('.coll_cont ul li a.f_link_b')  # webpage 보고 복습 !
for link in news_link:
    print(link.get('href'))


# id 로만 찾으면 안되는 이유!
print()
for link in soup('a', attrs={'id':'clusterresultUL'}):
    print(link.get('href'))
# id = clusterresultUL 이 어디 있을 지 모르기 때문에 범주를 정해서 down 시켜 id 를 범주화해야 한다.
```

