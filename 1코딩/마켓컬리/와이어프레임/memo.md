- 학습 목표: 기존 사이트의 구조를 분석하고 HTML·CSS로 최상단 배너 구현하기

# 실습 준비
1. HTML 파일을 Live Server로 실행한다.
2. HTML 기본 구조를 만들고 문서 언어를 한국어로 설정한다: <html lang="ko">.
3. 문서 제목을 마켓컬리 와이어프레임으로 변경한다.
4. <link rel="stylesheet" href="style1.css">로 CSS 파일을 연결한다.
style1.css는 예시 파일명이다. 실제 저장한 CSS 파일명과 일치해야 한다.


# 웹사이트 분석 방법
1. 마켓컬리 홈페이지에서 F12를 눌러 개발자 도구를 연다.
2. 요소 선택(화살표) 도구로 최상단 보라색 배너를 클릭한다.
3. 해당 요소의 클래스명과 CSS 속성을 확인한다.
4. AI에게 영역 명칭, 적절한 클래스명, 높이 및 배경색을 질문한다.
   - 해당 영역의 일반적인 명칭: 최상단 프로모션 배너(Top Banner)
   - 클래스명 예시: top-banner
   - 강의에서 안내한 배너 높이: 42px
   - 참고 배경색: #5F0080 (정확한 값은 원본 사이트의 개발자 도구에서 확인)


# HTML·CSS 핵심 문법
문법	의미
<div class="top-banner">	배너 영역을 만드는 HTML 요소
.top-banner	CSS의 클래스 선택자 (. 사용)
height: 42px;	높이를 42픽셀로 설정
background-color: #5F0080;	배경색을 보라색으로 설정
lang="ko"	문서 주 언어를 한국어로 지정

# 목표: 최상단 배너를 마무리하고, 회원가입·로그인·고객센터 유틸리티 메뉴를 구현한다.
## 최상단 배너 완성 
- 검정색으로 보이던 배너 문구를 color: #fff;로 흰색 처리.
- Flexbox는 정렬하려는 자식 요소의 부모에 적용한다.
- justify-content: center는 가로, align-items: center는 세로 중앙 정렬.
- 배너 글자 크기는 font-size: 14px로 설정.
.top-banner {
  height: 42px;
  background-color: #5F0080;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 14px;
}
배경색 #5F0080은 이전 강의에서 사용한 참고값이다. 강의 (2) 스크립트에는 정확한 색상 코드가 다시 나오지 않는다.

## Pretendard 웹폰트 적용
1. 눈누에서 Pretendard 폰트의 웹폰트 적용 코드를 찾는다.
2. 제공된 @font-face 또는 웹폰트 연결 코드를 CSS 최상단에 붙여 넣는다.
3. body에 font-family를 지정하여 페이지 전체에 적용한다.
4. 웹폰트가 로드되지 않을 때를 대비해 sans-serif를 대체 폰트로 지정한다.
/* 먼저 Pretendard 웹폰트 연결 코드를 추가 */
body {
  font-family: 'Pretendard', sans-serif;
}
- head: 문서 메타데이터와 외부 리소스 연결 등
- body: 화면에 표시되는 주요 콘텐츠
- 웹폰트 연결과 font-family로 폰트를 적용하는 과정은 구분한다.
3. 상단 유틸리티 메뉴 구조 (09:39~18:56, 34:55~37:40)
개발자 도구 F12 → 요소 선택 → 클래스 확인 → AI에 영역 명칭/스타일 질문. 해당 영역의 일반적인 명칭은 유틸리티 메뉴(Utility Menu).

메뉴는 회원가입, 로그인, 고객센터 세 항목으로 구성한다. 메뉴에는 nav, 목록에는 ul, 각 항목에는 li를 사용한다.
<div class="utility-menu">
  <div class="con">
    <nav>
      <ul>
        <li class="signup">회원가입</li>
        <li>로그인</li>
        <li>고객센터</li>
      </ul>
    </nav>
  </div>
</div>
- ul>li*3은 li 요소를 세 개 만드는 Emmet 문법.
- 실습에서는 텍스트로 구조를 먼저 만들었다. 실제 이동 기능을 만들 때는 각 항목 안에 <a> 링크를 넣는 것이 적절하다.
4. 고정 너비 컨테이너와 가운데 정렬 (26:01~33:22)
- 화면 폭이 달라도 메뉴 영역을 중앙에 배치하기 위해 내부 컨테이너 .con을 추가한다.
- 강의에서 사용한 너비는 1050px, 높이는 35px.
- margin-left: auto; margin-right: auto;로 좌우 바깥 여백을 자동 분배해 컨테이너를 중앙에 둔다.
- 부모와 자식 모두에 height를 중복 적용하지 않고, 가능한 내부 컨테이너 높이를 기준으로 부모 높이가 따라오도록 한다.
.con {
  width: 1050px;
  height: 35px;
  margin-left: auto;
  margin-right: auto;
}
위 너비는 강의 실습 값이다. 작은 화면까지 대응하는 반응형 구현에는 별도 보완이 필요하다.

## 유틸리티 메뉴 오른쪽 정렬과 목록 스타일 초기화
/* ul/li의 기본 여백과 목록 표시 제거 */
ul, li {
  margin: 0;
  padding: 0;
  list-style: none;
}

/* 컨테이너 내부 메뉴를 오른쪽으로 정렬 */
.utility-menu .con {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

/* 메뉴 항목을 가로로 배치하고 12px 간격 지정 */
.utility-menu .con > nav > ul {
  display: flex;
  gap: 12px;
}

/* 회원가입만 별도 강조 (예시 색상) */
.signup {
  color: #5F0080;
}
- justify-content: flex-end: 가로 오른쪽 정렬.
- align-items: center: 세로 가운데 정렬.
- gap: 12px: Flexbox 항목 사이 간격.
- ul, li의 브라우저 기본 여백 및 목록 마커 제거는 수업에서 노멀라이즈(normalize) 작업으로 설명함.
- 회원가입만 색을 바꾸려면 세 항목 전체가 아니라 특정 항목에 클래스를 지정한다.
- .con > nav > ul의 >는 직계 자식 선택자이다.