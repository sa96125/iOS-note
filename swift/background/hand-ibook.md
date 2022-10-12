---
description: 사소하지만 알아두면 쓸대 있는 iOS 지식을 질문하고 답합니다.
---

# Hand ibook

* 애플 개발은 맥에서만 가능할까? 맥북외에도 개발환경을 구성할 수 있는 방법이 있다! hackintosh 또는 macin clould을 사용하면 맥북이 없더라도 개발이 가능하다. 단, 애플은 자체 소프트웨어를 다루는 것, 이 소프트웨어가 구동되는 환경에 매우 엄격하기 때문에 실제 기기를 연동하는 작업이 어려울 수 있다.



* 시뮬레이터와 실제기기의 차이점은 무엇일까? Virtual Device는 모든 기능을 지원하지 않는다! notifications, apple Health와 같은 것들은 시뮬레이터에서 테스트할 수 없다.



* 내 앱을 굳이 iOS로 개발해야할까? 단지, 화면의 정보를 표현하는 앱이라면 반응형 웹으로 개발하는 것이 시간과 돈을 절약하는 효율적인 방법이 될 수 있다. 하지만, 아이폰 기기의 기능을 활용해야한다면 아주 칭찬해\~



* 프로젝트 조직명은 어떻게 작성할까? Organization Identifier옵션은 일반적으로 회사 도메인의 반대로 적는게 일반적이다! 회사라면 도메인을 가지고 있을 테고 이 Url은 고유하니까\~:)



* X-code의 각 구역의 명칭은 뭘까? 상단 Status bar 좌측 Navigator, 우측 Inspector, 중앙 code Editor, 하단 Debug area, 디자인 파일 내부는 Document Outline과 Interface Builder로 구성된다.



* 디자인 파일의 캔버스 종류를 선택할 때, 왜 특정 버전의 아이폰은 보이지 않는 걸까? 몇몇 아이폰은 공통된 Aspect Ratio를 가지고 있다. 그 예로 6, 7, 8 그리고 SE2는 4.7인치 스크린을 쉐어하고 있다. 따라서 굳이 모든 버전을 나타내지 않는다.



* iPhone 해상도의 단위는 무엇일까? 애플의 해상도 표기 pixel 단위가 아니다. 아이폰 2,3의 경우 320 x 480 points x1 해상도를 가지고 있는데 이는 해상도의 1을 곱한만큼의 pixel로 렌더링됨을 의미한다., 4 \~ 8은 해상도의 2배(Retina), Plus 또는 Max의 경우 3배의 pixel을 표한하고 이를 rasterization이라고 한다. 같은 스크린일지라도 배율이 높을 수록 더욱 촘촘하게 pixel이 압축되어있기때문에 확대를 하더라도 이미지의 훼손이 없어보이고 더 선명한 이미지를 보여줄 수 있다. 만약 내가 사용하는 이미지가 300pixel이면, 애플환경에서는 최대크기가 100pixel로 압축되어 보여질 것이다.



* 왜 많은 Appicon이미지가 필요한걸까? 아이콘의 사용 용도가 다르기 때문이다. 앱스토어, 알림, 셋팅, 스팟라이트등 다양한 곳에서 아이콘이 사용되고 있다. 하나의 이미지를 사용할 수 있는 것 아닌가라고 생각할 수 있지만 사실 속도와도 연관성이 있다. 하나의 이미지를 다운사이즈할 때 자칫 앱을 느려질 수 있으므로 미리 다양한 사이즈를 준비하여 이를 예방한다.



* Xcode의 개발한 것을 실제 기기에서 테스트하기 전 필수확인 사항은 무엇일까? x-code version과 iphone os version의 소수점 첫 자리가 일치해야한다는 사실! 기억하자