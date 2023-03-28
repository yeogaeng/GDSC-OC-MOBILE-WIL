# WIL1

Created by: 고여경
Created time: 2023년 3월 28일 오후 8:30
Last edited by: 고여경
Last edited time: 2023년 3월 28일 오후 8:56
URL: https://nomadcoders.co/dart-for-beginners/lobby

# #0. Dart란

# 다트: 플랫폼

Dart의 컴파일러 기술을 사용하면 다양한 방식으로 코드를 실행할 수 있다.

- **기본 플랫폼** : 모바일 및 데스크톱 장치를 대상으로 하는 앱의 경우 Dart에는 JIT(Just-In-Time) 컴파일 기능이 있는 Dart VM과 머신 코드 생성을 위한 AOT(Ahead-of-Time) 컴파일러가 모두 포함되어있다.
- **웹 플랫폼** : 웹을 대상으로 하는 앱의 경우 Dart는 개발 또는 프로덕션 목적으로 컴파일할 수 있다. 웹 컴파일러는 Dart를 JavaScript로 변환한다.

![Untitled](WIL1%20286d12390aa6413382f20cd90b215ded/Untitled.png)

Flutter 프레임워크는 인기 있는 다중 플랫폼 UI 툴킷으로 Dart 플랫폼으로 구동되며 iOS, Android, macOS, Windows, Linux 및 웹에서 실행되는 UI 경험을 빌드하기 위한 도구 및 UI 라이브러리를 제공한다.

### 다트 네이티브(기계 코드 JIT 및 AOT)

**개발할 때는 JIT를 쓰고, 프로모션 때는 AOT**를 쓴다. 

JIT를 쓸 때, 머신코드로 안 바꾸고 VM(가상머신)에서 컴파일해서 결과를 즉각적으로 화면에서 볼 수 있다. 

앱을 프로덕션에 배포할 준비가 되면(앱 스토어에 게시하든 프로덕션 백엔드에 배포하든) Dart AOT(ahead-of-time) 컴파일러가 기본 ARM 또는 x64 머신 코드로 컴파일할 수 있다. AOT로 컴파일된 앱은 매우 빠르다.

# #1. VARIABLES

## #1.1 The Var Keyword

```dart
var name = '여경'
String name1 = '여경'
name1 = '준혁' //변수 변경가능
```

-관습적으로 `var` 은 함수나 메소드 내부에 지역 변수를 선언할 때 사용하고, 

`String` 같이 타입이 지정된 변수는 class에서 변수나 property를 선언할 때 사용한다.

## #1.2 Dynamic Type

```dart
dynamic name;
if(name is String){//if문 안에서는 name이 String 일 때를 알려줌. 
//타입을 정해줘야 메소드 추천을 해줄 수 있다!
}  
```

-여러 가지 타입을 가질 수 있는 변수에 쓰는 키워드이다. 

-추천은 하지 않고, 필요할 때만 써야한다. 

-타입을 정해줘야 메소드 추천을 해준다.

## #1.3 Dynamic Type

-null safety : 개발자가 null 값을 참조할 수 없게한다.

```dart
bool isEmpty(String string) => string length == 0;
main(){
	isEmpty(null);
}
//No SuchMethodError!
```

isEmpty가 null 값이라 length를 가져올 수 없어 에러가 뜬다.

⇒ null 값을 보호해야한다. 어떤 변수가 null이 될 수 있음을 명시해야한다.

```dart
String? nico ='nico';
nico = null;
if(nico!=null){
	nico.isNotEmpty;
}
nico.isNotEmpty; //이것도 됨
```

null 값을 넣고 싶으면 `?`가 꼭 필요하다.

## #1.4 Finial Variables

```dart
final name = '여경'
```

한 번 정의된 변수를 수정하지 못하게 한다.

## #1.5 Late Variables

```dart
late final String name;
name = ''; //이게 없으면 error뜸
print(name);
```

-final 이나 var 앞에 붙여줄 수 있다.

-late는 초기 데이터 없이 변수를 선언할 수 있게 해준다.

late로 변수를 선언하고 중간에 api같은 값을 받아서 나중에 값을 할당해주는데 사용할 수 있다.