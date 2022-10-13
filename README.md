# Background

애플의 최대 행사 WWDC 2014에서 처음으 Swift가 소개되었습니다. 진입 장벽이 높았던 Objective-C를 대체하려는 목적으로 개발되었습니다. 덕분에 애플 환경에서 더욱 쉽게 앱을 개발할 수 있습니다. 기존 Objective-C에 없던 새로운 기능(closure, generic, type inference)이 추가되었고 쉬운 사용성으로 인해 애플 생태계로 확장성이 높아졌습니다.





처음 공개되었을 당시 Swift는 Safe, Modern, Powerful 한 프로그래밍 언어로 소개되었으나 오픈소스로 전환하며 Swift를 대표하는 문구가 **Safe, Fast, Expressive**로 변경되었습니다.&#x20;

첫 번째로 매우 안전한 프로그래밍을 지향하는 언어답게 옵셔널, 가드, 타입 통제, 오류처리를 사용하며 강력한 안정성을 구축하고 있습니다. 또한 C 언어에 준하는 성능을 유지하는 데 초점을 맞추어 개발되어 매우 빠릅니다. 실행 속도 최적화뿐만 아니라, 컴파일러를 지속적으로 개량하여 더욱 빠른 성능을 구현해가고 있습니다.&#x20;





또한, Swift는 여러 프로그래밍 패러다임을 차용한 **다중 패러다임 프로그래밍 언어**입니다.&#x20;

1. 객체지향(OOP), 프로그램을 일련의 명령의 순서로 보는 명령형 프로그래밍 패러다임에서 벗어나 여러 개의 독립된 단위인 객체의 모음으로 보는 시각입니다.&#x20;
2. 함수지향(FP), 프로그램의 상태 변화 없이 데이터 처리를 수학적 함수 계산으로 취급하는 방식의 패러다임으로 값의 변화에 집중하지 않고 순수 기능 자체를 중요하게 생각합니다.&#x20;
3. 프로토콜 지향(POP), 프로토콜을 사용하면 클래스보다 더 안전한 추상화 메커니즘을 구현할 수 있습니다. Swift에서는 구조체와 열거형에 기존의 클래스에서 구현할 수 있었던 캡슐화, 추상화, 접근 제어 등의 기능을 모두 구현할 수 있습니다.
