# WIL3

Created by: 고여경
Created time: 2023년 4월 12일 오전 3:05
Last edited by: 고여경
Last edited time: 2023년 4월 12일 오전 3:51

# Flutter 위젯

# MaterialApp() vs. Cupertino()

Material Design 은 구글에서 지원하는 디자인 패키지로 Android 플랫폼에서 지원하는 대부분의 기본 UI 컴퍼넌트를 제공하며, Cupertino Design은 애플에서 지원하는 디자인 패키지로, iOS플랫폼에서 지원하는 대부분의 기본 UI 컴퍼넌트를 제공한다.

## MaterialApp()을 사용하기위해(커스터마이징을 원해도)

⇒ import ‘package:flutter/material.dart’ 를 추가하기

## Cupertiono()를 사용하기위해(애플스러운 디자인을 원한다면)

⇒ import ‘package:flutter/cupertino.dart’를 추가 

### [Scaffold 위젯 : 앱을 상중하로 나눠줌]

-appbar : AppBar()

-body : Container()

-bottomNavigationBar : BottomAppBar()

column, row에서 

.spaceEvenly 잘 쓰기.

---

# Dart 공부

# #4. Classes

변수는 var 로 타입을 안 정해도되지만, class는 타입 설정이 중요하다.

```dart
class Player{
	String name = 'nico';
	int xp = 1500;
	void sayHello(){(print("Hi my name is $name");} 
//원래 다른 언어에서는 ${this.name}으로 쓰지만, dart에서는 class내부에서 선언한 변수를 print로 부를 때 this를 사용하지 않는 것을 권고한다. 
}

void main(){
	var player = Player();
	player.name = 'lalala'; //Player호출해서 player 인스턴스 하나가 생성됨
	print(player.name);
	play.sayHello();
}

```

## #4.1. Constructor 생성자

class가 모든 player의 이름과 xp가 같아서 재미가 없다~  argument 로 player이름, xp를 전달하고싶을 때

Player라는 Class에

```dart
Player(String name, int xp){
		this.name = name;
		this.xp = xp;
	}
```

를 추가하고 싶다면, 아직 값을 설정하지 않은 변수를 생성자에 넣어주므로 class에서 선언한 변수 타입 앞에 **late**를 붙여야한다.

```dart
class Player{
	**late** final String name;
	**late** int xp = 1500;
	Player(String name, int xp){ //새로 추가한 게 여기
		this.name = name;
		this.xp = xp;
	}
	void sayHello(){(print("Hi my name is $name");} 
}

void main(){
	var player = Player("nico', 1500); //positional parameters
}

```

코드를 줄이자면, 

```dart
Player(this.name, this.xp}; //새로 추가한 걸 이렇게 바꿀 수 있다.
```

마지막 main()에서 positional parameters를 사용했는데, class가 커지면 positional은 통제하기어렵다.

## #4.2 Named Constructor Parameter

positional ⇒ Named 방법은 

{} 로 감싸는것이다.

```dart
Player({required this.name, required this.xp, required this.team, required this.age});

var player=Player(
	name: "nico",
	xp: 1200,
	team: 'blue',
	age: 21,
);
```

## #4.3 Named Constructors

```dart
class Player {
	final String name;
	int xp, age;
	String team;

	Player ({
		required this.name,
		required this.xp,
		required this.team,
	  required this.age,
	});

	Player.createBluePlayer({required String name, required int age}): //:으로 일대일 초기화
		this.age = age,
		this.name = name,
		this.team = 'blue',
		this.xp=0; 

}

void main(){
	var player = Player.createBluePlayer(
		name : "nico",
	  age: 21,
}
```