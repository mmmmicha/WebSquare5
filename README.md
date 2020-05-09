# WebSquare5_Study

webSquare5_Document link : https://wtech.inswave.kr/websquare/websquare.html?w2xPath=/ws/index.xml&inPath=edu

일시 : 2020-04-23 ~ 2020-04-24

- <b>웹스퀘어5(Websquare5) 란?</b>    

   > - 국내 최초의 WYSIWYG 개발 도구가 포함된 HTML5 웹 표준 UI 플랫폼으로 최신의 선진 신기술과 개념, 다양한 구축 경험과 방법론을 집대성하여 HTML5를 완벽히 지원할 수 있는 HTML5 웹표준 UI 플랫폼. 
   > - No Active X, No Runtime, Only Standard 를 가능케 함.
   
   > - 특징<br>
       1. Open Architecture<br>
       2. HTML5 Standards 적용<br>
       3. Adaptive Web Component 제공<br>
       4. One Source Multi Use 지원<br>
       5. 통합개발도구 지원
     
   > - DataCollection 이란?<br>
       1. 데이터 객체들의 저장소(서버와 통신하기 위한 request, response 객체와 UI구현을 위한 임시 데이터 객체들이 존재)<br>
       2. 데이터 객체의 종류 : DataMap, DataList, LinkedDataList<br>
       3. 각 객체는 JSON, XML, 1차원 Array 형태의 데이터로 설정하거나 변환이 가능<br>
       4. 각 객체는 id 가 필수<br>
       5. script 에서의 객체 접근은 객체의 id명으로 가능하며 DataCollection(최상위)에 접근하는 경우는 $w.data 객체를 사용함
     
   > - Data 객체의 종류<br>
       1. DataCollection<br>
          - Data 객체를 담는 최상위 객체로 그롯에 해당<br>
          - $w.data로 접근이 가능하며 전체 데이터 객체를 제어할 수 있음<br>
          - Java의 Map 과 흡사<br>
     
       2. DataMap<br>
          - Key와 Value로 이루어진 단일 데이터의 객체<br>
          - Java의 Map 과 흡사<br>
        
       3. DataList<br>
          - List 형태의 다건의 데이터로 구성된 객체<br>
          - Java의 List 와 흡사<br>
        
       4. LinkedDataList<br>
          - DataList 객체를 참고하여 Filter, Sort를 적용한 객체<br>
          - 기준되는 DataList 객체가 꼭 필요

   > - Submission 이란?<br>
       - ajax로 구현되어 있는 통신 모듈<br>
       - 일반적으로 request, response 데이터는 DataCollection에 정의한 데이터 객체와 연동<br>
       - request는 reference로 표현<br>
       - response는 target으로 표현 및 표기 됨

------------------------------------------------------------------------------------------------------------------------------

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
  <![CDATA[<servlet>
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
	   </servlet-mapping>]]>

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

<h2>2일차</h2>

- textbox 와 span 의 차이
  긴거 쓸 경우, 짧은거 혹은 변화가 잦은거 쓰는 경우

- Controller 를 어떻게 설정하느냐에 따라 input을 한꺼번에 주어 submission 을 한번만 수행할 수도 있음.(submission 을 여러번 수행하는 것도 결국 자원소모이기 때문에 될 수 있으면 적은 submission 으로 데이터 교환을 해결하는게 좋다)
  TrainingController.java 꼭 확인하기!!!

- eduCommon.js 에 setCommonCode 메소드 확인해보기
  알아서 DataCollection 생성해주고 데이터 매핑 해주고 submission 까지 해줌.(이건 공용프로그램개발자들이 주로 건드림. WRM 교육 받게되면 이런것들도 배울 수 있음)

- getvalue 로 직접 값을 설정하기보다 ref 를 적극적으로 활용할것!!!
  (ref 또는 setNodeSet())

- GridView ?? 실질적으로는 그저 display 역할 뿐
  - 진짜매우중요!! 얘는 DataList 라는 짝꿍이 있다. 그냥 DataList 가 전부다.
  - gridview 에 DataCollection에서 원하는 것을 드래그해서 놓으면 자동으로 매핑까지 다 해줌

  - autoFit 이라는 속성이 있음
  - 반응형웹을 위해서 autoFitMinWidth도 설정해야함 (보통 700)
  - rownum 이라는 속성이 있음 (true 면 rownum 이 보임)
  - rownum 과 관련된 편집은 무조건 rownum 이 붙은 속성들로 컨트롤 해야함
  - sort 기능도 있음.
  - sortEvent 로는 원클릭, 더블클릭을 설정할 수 있음.
  - grid 전체적으로 말고 셀자체만도 sortable 을 설정할 수 있음.
  - filter 속성도 있음.(셀만지정할 수도 있고, grid 속성으로도 할 수 있음)
    (필터를 콤보박스로 사용하고 싶으면 우선적으로 컬럼을 지정해서 filter 설정을 한 후에 grid 에서 useFilterList 까지 true 로 해줘야 한다)
  - readOnly 속성도 있음(각 컬럼)
  - focusMode 라는 속성이 있음(컬럼전체 또는 로우전체 등등)
  - 정렬(align) 속성도 있음
  - displayFormmat 이라는 속성도 있음(ex. ###-### 등)
    (로직이 들어가서 경우에 따라 다르게 표현해야 할 때는 안됨!!)
  - displayFormmatter는 이를 표현할 수 있음(함수를 직접만들어서 사용하는 것임)
  - columMove 라는 속성이 있음(자유자재로 바꿀 수 있음 페이지 내에서)
  - 고정은 fixed

  - 중요 datamapping 을 component 랑 collection 을 해놨을 때, 페이지내에서 데이터를 바꾸게 되면 조회되는 데이터도 바뀐다. 이를 방지하기 위해서는 readOnly등이 필요하다.

  - 중요!! 데이터를 조작하는 것은 무조건 DataList 다.
  - rowState 는 CRUD 를 나타내주는, 자동적으로 만들어지는 행이다.(페이지에서 웹스퀘어5 지원페이지에서 확인할 수 있음)
  - 이와 연관되어 있는 property 는 rowstatusVisible 이다.

  - delete 는 일종의 마킹만 하는 거고
  - remove 는 진짜로 데이터를 삭제하는 것이다.
  
  - check 박스를 다루는 과정에서 ignoreStatus 라는 속성이 있다.
    (true 이면 CRUD 를 표시하지 않음.)

  - DataCollection 에도 이벤트를 적용할 수 있다. 가령 데이터가 바뀐다거나 할 때 일어나는 이벤트 등등...

  - 중요!! grid의 컬럼을 변경하려면 dataList 를 재정의한 후에 grid 를 다시 업데이트 해야한다.
  - 컬럼명 들어가는 곳에 checkbox 로 하면 전체 선택기능도 사용할 수 있음.

  - removeAll 이라는 API 가 있다.

  - dataCollection을 만들 때 action 속성 'modified' 를 지정하면 데이터가 변경됐는지 여부를 확인할 수 있다.

  - grid 를 엑셀로 변환해서 내릴수 있는 기능이 있다.

  - 엑셀 연동 기능에서 hidden 속성을 사용하게 되면 페이지에서는 해당 속성이 보여지지 않지만 엑셀로 다운로드 할 때는 표현이 된다.(ex. 주소2)
  - hidden 해놓고 디자인 탭에서 뭘숨겼는지 보려면 마우스 우클릭해서 숨긴셀 보기 할 수 있다.

  - footer 만들기
    - 그리드에 마우스 우클릭 후 footer 추가 클릭
    - 급여 컬럼 속성 확인하기!!!( ,inputtype, expression)

    - 더 디테일하게 소계, 중계 처리같은 경우는 또다른 property를 적용할 수 있다.


** 선생님의 조언

   - 페이지구현 part 에 4번에는 scrollEnd 이벤트를 이용하여 만든 흥미로운 예제가 있다.

-------------------------------------------------------------------------------------

- 브리핑자료 추가할 예정
