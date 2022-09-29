# MVC

model-view-controller 디자인 패턴은 쉽게 말해 데이터와 이를 처리하는 로직을 담는 영역, 인터랙션을 담당하는 유저 인터페이스 영역 그리고 이를 중재하는 영역으로 나눈 것을 말한다. 모델과 뷰는 직접 관여하지 않고 컨트롤러에 의해서 상호작용을 할 수 있게 된다. 만약 화면 속에서 다양한 내용을 표현하고 싶을 때, 모델 부분만 다르게 처리하여 코드를 재사용할 수 있는 이점이 생긴다. 뿐만아니라 분리하여 컴포넌트를 관리가능하니까 나뿐만 아니라 다른사람들이 보기에도 프로그램이 훨씬 읽고 이해하기 쉬워진다.

1. send event
2. makes request
3. send back data
4. modifies UI

실제 코드를 작성한 뒤 MVC패턴으로 코드를 리팩토링할 수 있어야한다. 먼저 Model을 구조체로 생성한 후, 기존 코드 로직을 객체의 메서드로 호출한다. 여기서 고려해야할 사항은 구조체 내에서 사용하는 변수를 굳이 생성자로 값을 받아 할당할 필요성이 있는가 하는 것, 또 초기화값이 굳이 할당되어야하는 것일까? 초기화 값이 필요 없다면 nil이 포함되는데, 옵셔널 변수는 값이 할당되지 않은채 값이 호출 될 수 있다. 즉 런타임 에러를 초래하지 않도록 고려되어야 한다.