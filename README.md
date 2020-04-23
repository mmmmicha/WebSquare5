# WebSquare5_Study

일시 : 2020-04-23 ~ 2020-04-24

<h2>1일차</h2>

- was 에러나는 경우

  - 2번째 was delete -> new server tomcat9 선택 -> 이름 ws5 -> server 탭 열어서 

- 2017년 부터 웹스퀘어5의 패턴들이 확 달라졌음. 그전꺼는 웬만하면 참고하지 말 것.

- 특징
  - xml 파일에서 디자인을 하게 되는데(뷰파일을 만들더라도 자동적으로 xml 확장자가 붙음)
  - 먼저 브라우저를 실행하게 되면 웹스퀘어 엔진을 먼저 로딩하게 되고 이 엔진이 xml 내 객체들을 html dom 으로 변환됨.
    (<w2: >, <xf: > 이 태그들을 변환함)
  - javascript 나 jquery 사용이 가능하지만, jquery 는 일부 충돌이 나는 경우가 있다.
  - 디자인도 그대로 css를 사용
  - **form 태그를 사용할 수는 있지만 ajax를 기본으로 사용함. --> submission 이라는 데이터통신모듈을 사용하게됨.
  - data를 매핑하는 측면에서 json, xml 형식의 데이터 다 호완됨
  - 화면소스스펙은 Xforms 을 따른다.
  - JDK 1.5 이상이면 사용가능하다.(J2EE 기반이면 다 된다고 보면 된다.)

  - 현재 배포되어있는 웹스퀘어5는 플러그인버전이 아닌 stand-alone 버전이다. 즉 자체 IDE.
  - 5대 브라우저 다 지원
  - 이건 xml 이라 was 에 올라가는것이 아니라 웹서버에 기본적으로 올라간다.(정적리소스)

  - Open Perspective 를 보면 designer 모드랑 publisher 모드로 나뉜다.

  - 환경설정되어있는 것은 java source 알아서 확인해보기.

  - **웹스퀘어 엔진**은 lib 에 jar 파일로 있다.(websquare_5.0_4.3993B.20200326.113812_1.5.jar)

  -  web.xml
  <!--     <servlet>
		<servlet-name>websquareDispatcher</servlet-name>
		<servlet-class>websquare.http.DefaultRequestDispatcher</servlet-class>
		<init-param>
			<param-name>WEBSQUARE_HOME</param-name>
			<param-value>C:\WRM\RESOURCE\WS5\websquare_home</param-value>
		</init-param>
	   </servlet>
	   <servlet-mapping>
		<servlet-name>websquareDispatcher</servlet-name>
		<url-pattern>*.wq</url-pattern>
	   </servlet-mapping>]-->

  - C:\WRM\RESOURCE\WS5\websquare_home\config 여기에 있는 websqaure.xml 이 환경설정 파일

  - 페이지 생성 : new -> websquare page

  - 모든 웹스퀘어 페이지들은 websquare.html 내 body 에 렌더링이 되는 개념이다.

  - javascipt 에서 scwin 의 하위로 메소드나 변수들을 사용하는 이유는 웹스퀘어엔진이 메모리관리를 자동적으로 해줌. 사용하고난 후 반납이라던가 이런것들.
   즉, scwin 을 전역객체로 default해놓음.

  ** 참고
     javascript 코딩을 할 때
    {
	var sc = "";
            function scc(){
            
	}
     }
   이런식으로 호출을 해 놓으면 데이터의 수명관리를 직접적으로 해줘야함.
   그렇기 때문에 객체를 하나 만들고 그 객체의 하위 변수 또는 하위 함수로 만들어서 부모객체를 컨트롤 하는 방법을 주로 사용한다.

  - onpageload : DOM 객체들이 모두 load된 후에 작동되는 메소드. init 함수 사용할 거면 onpageload 에 사용할 것!!! 강조!!!
    (init 을 쓰게되면 DOM 객체들이 제대로 load되지도 않았는데 그 내부 객체들을 불러내는 호출이 일어나는 것이기 때문에 에러가 생긴다.)
  - js 나 css import 하기 위해서는 그냥 design view 에 파일을 드래그해서 넣으면 소스에 적용이됨.
  - datatype default 형은 text

  - 기본적으로 내장하고 있는 Editor 는 CKEditor
    (OEM 으로 Editor 를 적용한거임)
    (OEM은 주문자의 의뢰에 따라 주문자의 상표를 부착하여 판매할 상품을 제작하는 업체를 의미한다.)

  - 각종 예시들을 제공해줌(websquare 교육 사이트!!)
  - button 을 쓰고 싶을 때는 trigger component 내 속성을 button 으로 사용하면 됨.
    (<a>를 나타내는 anchor, <image>를 나타내는 image 도 가능하다.)

  - 업로드에 대한 설정은 websquare.xml 에 초기 설정에 되어있으니 확인할것.
  - 멀티업로드는 flash 내지 html5_transport

  - project explorer 에서 ctrl+shift+r 단축키는 파일 찾기

  - div 는 group 이라는 component 가 대체
    (component 를 group 짓게 되면 css 를 적용해서 일괄적인 control을 하는데 매우 유용하다.)

  - generator 와 grid 의 차이
    - 댓글관리도 generator

  - IFrame 대신 WFrame 을 쓴다.
    - WFrame 은 페이지를 import 하는 개념
    - WFrame 에 스콤이라는 기능을 넣어놨는데 이는 자식과 부모간의 id중복을 막아준다.

    - IFrame 은 요소들을 사용할 때 중간중간 필요하지 않은 컴포넌트들을 사용하게되면서 메모리 누수와 효율성이 떨어진다. 반면에 WFrame 은 그게 없어서 빠르고 간결하다.

  - TabContainer 대신에 TabControl 을 사용한다.

  - layer 팝업(주소가 안뜸) vs 윈도우 팝업(주소가 뜸)
    - 일단 웹스퀘어에선 둘다 사용이 가능하다.

  - 이론문서에 보면 'UI Design' 파트가 있음.
     - 여기에 static/absolute position 이 있음.
        (도형을 자유자재로 위치조정을 할 수 있게 만들거나 아니면 고정적으로 하거나)
        하지만 absolute 는 가급적 사용하지 않는게 좋다(랜더링하는게 뒤죽박죽될수 있고 이는 ux측면에서 아주 안좋음)
  - snippet 이라는 효율적인 모듈화 기능이 있다.(import/export 가 가능하다)
    (보통 publisher가 이를 만들어서 export 해주면 개발자가 import 해서 사용한다.)

  - 웹 렌더링에는 block 단위와 inline 단위가 있다.
  - css overflow 속성에대해 알아보기

  - 이미 xml 내 그려놓은 컴포넌트 클릭하고 space바 누르면 퀵셋팅 기능이 있음
  - f2 는 부모선택 단축키

  - adaptive 가 반응형웹을 랜더링하는 속성(adaptiveThreshold 도)
    layout 모드를 사용하는것이 반응형웹을 사용하는것이며, crosstab의 경우 thead 등등을 사용해야해서 복잡하다.
  - id 설정할때 '_' 외에 다른 특수문자는 쓰지말것! 특히 그냥 '-' 이거(javascript 가 빼기 로 인식할 가능성이 매우 높음)
  
  - $p 를 쓰면 유틸성 API 들을 쓸수있다.

  - $blank 는 select component를 다룰 때 빈칸을 설정할 수 있는 명령문
    
  - min- : prefix 이거는 width 나 height 를 보정해주는 prefix
  - 라디오버튼 component를 더블클릭하면 row정렬 cols 정렬을 지정할 수 있음(즉, 배치를 가로로 할 것이냐, 새로로 할 것이냐)

  - 브라우저에서 ctrl+우클릭(웹스퀘어5 에서 지원하는 기능)
  - dataList 에서 rowStatus 는 CRUD 를 나타내준다.

  - **중요** Submit-done 에서 콜백함수 설정을 할 수가 있음. 그래서 synch 가 아니어도 비동기방식으로 순서제어를 할 수가 있음.

  - Add submission 에서 Instance, Replace 는 지금은 사용안한다. 무시하면 됨.
  - Custom Handler 는 전처리기(서버로 보내기 직전에 사용됨) - 근데 잘 사용안함,
    Error Handler 는 후처리기(200미만 400이상일 땐 안됨) - 직접작성할일 거의없음(공통개발자가 작성함)
  - processMessage : 조회중... (통신하는동안 로딩중을 주고 disable이 되어버려서 다른 것들에서 접근이 불가능해짐)

  - Submit, -done, -error 는 우리가 직접 작성하는 전처리, 후처리 에러잡아내는 것

  - defaultValue 는 빈칸일때 되는 값
  - DataCollection 에서 useData 옆에 있는 버튼은 mapping 을 해주는 버튼 (defaultValue 랑 같은 역할)  
  - dc_reqUserInfo.setValue() 로도 가능

  - Edit submission 에서 single mode 누르지 말것. 이거 누를경우에 target하나로 데이터를 교환해버려
  - controller 에서 받는 데이터와 view 에서보내는 데이터의 이름이 같아야하는건 기본인데 만약 view 딴에서 다르게 하고싶은 경우 설정을 달리할 수 있음!! DataCollection 에서 할 수 있다.
  
  - WFrame 을 사용했을 때 자식과 부모의 id가 중복되지 않게 하는 scope 의 기능이 있다.
    scope 를 굳이 직접설정하지 않아도 config.xml 에 자동으로 설정이 되어 있음.

    여기서 진짜 중요한게.. 자식페이지랑 부모페이지에 id 에 대한 접근을 할 때 자체적으로 바꿔준 id로 써주는게 아니라 고유로 쓴 id로 접근하면 된다.

    t1.getWindow(0) 이건 자식 페이지 접근할 때
    $p.parent() 이건 부모 페이지 접근할 때
    예제 : http://127.0.0.1:8080/ws5/?w2xPath=/ws5/sample/pageScope/master.xml 이게 예제

  - AliasDataMap, List 는 자식에서 부모의 DataCollection 을 바라보고 싶을 때 사용하는 것이다.
    속성은 scope, studioSrc 설정해야 한다.
    scope : 부모 DC 의 id ex) ../dataMap1 꼭!! 상대경로 또는 절대경로로 표시를 해줘야 한다. 그냥 dataMap1 으로 하면 브라우저상에서 확인을 해볼수 없다.
    studioSrc : 부모 페이지 url ex) /ws5/parent.xml
    예제 : http://127.0.0.1:8080/ws5/?w2xPath=/ws5/sample/pageScope/master_alliasData.xml
    주의!! 자식에서 부모만 바라볼 수 있다. 부모에서 자식은 안됨.

    예제 : http://127.0.0.1:8080/ws5/?w2xPath=/ws5/sample/pageScope/wframeScope.xml
    이건 자식의 자식의 자식의 자식 예제

