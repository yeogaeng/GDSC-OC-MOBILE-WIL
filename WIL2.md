# WIL2

Created by: 고여경
Created time: 2023년 3월 30일 오후 1:37
Last edited by: 고여경
Last edited time: 2023년 4월 4일 오후 1:38

# Dart

# #2 DATA TYPES

dart는 모두 object로 이루어져있다. int, double, ..과 같이 우리가 알고있던 type들이 정의로 들어가보면, num으로부터 상속되어있는 것을 볼 수 있다.

```dart
num x=12;
x=1.2;
```

num은 모든 타입이 다 된다고 생각하면 된다.

## #2.1 Lists

```dart
var numbers=[1,2,3,4,]
List<int>numbers = [1,2,3,4,];
numbers.add(1);

print(numbers.first); //첫번째 요소
print(numbers.last); //마지막 요소
print(numbers.isEmpty); //list가 비어있는지 확인해줌
```

collection if / collection for

### collection if

: if로 존재할수도, 존재 하지 않을 수도있는 요소를 만들어준다.

```dart
var giveMeFive = true;
var numbers = [
	1,
	2,
	3,
	4,
	if(giveMeFive) 5, //if(giveMeFive){numbers.add(5)}와 같다.
];
print(numbers);

```

## #2.4 Maps

python의 dictionary, js의 object와 비슷하다.

```dart
var player = {
	'name' : 'nico',
	'xp' : 19.99,
	'superpower' : false,
};
```

var에 마우스를 올려두면 입력한 값에 따라, 타입이 <String, Object> 로 뜨는 것을 확인할 수 있다. 여기서 object는 모든 타입이 될 수 있다고 생각하면 된다. ( js의 any와 유사하다. )

위의 코드처럼 작성한다면 compiler가 key와 value 타입을 유추해준다.

```dart
Map<int,bool>player = {};
```

아래처럼 map, type을 명시해줄 수 있다.

하지만, key, value, object 이런게 있다면 Map보다는 class를 쓰는것이 더 좋다.

## #2.5 Set

파이썬의 tuple 과 같다.

```dart
var numbers = {1,2,3,4};
```

```dart
Set<int>numbers = {1,2,3,4};
numbers.add(1); //결과값 {1,2,3,4} . 중복된 값 취급 x
```

모든 아이템이 unique 한 것이 list와 다른 점이다.

# #3 FUNCTIONS

-함수에서 바로 return 하는 함수면

`String sayHello(String potato) ⇒ “Hello $potato nice to meet you”;`

`⇒` 으로 바로 함수를 표현할 수 있다.

## #3.1

named parameter를 지원

null safety를 위해 default value를 적어주거나 required modifier를 쓰자.

```dart
String sayHello(required String name, required int age, required String country,){
return "Hello $name, You are $age, and you come from $country");

void main(){
	sayHello(); ->error //required가 있으니까 compile 해주지 않는다. null safety
}
```

## #3.2 parameter

positional parameter : 순서가 중요하다. 다른 파일에서 보내줄 때 뭔지 바로 파악하기 어려워서 좋은 방법이 아니다.

named parameter

## #3.3 optional = positional parameter

하나의 argument만 main에서 함수로 안 보낼때.

```dart
String sayHello(String name, int age, [String? country='Cuba'])
=> "Hello $name, You are $age, and you come from $country";
```

1. 대괄호

2. country를 인자로 안 보내주는 경우를 생각해서 `?` 를 사용하고 그에 따른 default값으로 Cuba를 넣어준다.

## #3.4 QQ(?, ??)

String capitalizeName(String?name) => name.toUpperCase(); 의 null값을 조심해서 한 줄 씩 변경시켜보겠다.

```dart
String capitalizeName(String?name) => name.toUpperCase();
//name이 null인 경우 안된다.
String capitalizeName(String?name) => name!=null?name.toUpperCase():'ANON'
//그래서 바꾼것이 ? : 삼항연산자같은 것 쓰기
String capitalizeName(String?name) => name.toUpperCase()??'ANON'
//근데 더 짧게 ?? 사용가능
```

`left ?? right` 인 경우,

if left가 null이면 right, left가 null이 아니면, right라는 의미이다.

그래서 `name.toUpperCase()??'ANON'` 의미는

name.toUpperCase()가 null이면 ‘ANON’, null이 아니면, name.toUpperCase()를 수행하면 된다.

`??`를 쓰는 다른 예시 : if name is null -> default 할 때

```dart
String? name;
name ??='nico'; //name이 null값일 때, nico를 넣어줌
```

## #3.5 typedef로 type을 지정해줄 수 있음.

```dart
void main(){
	typedef ListOfInts = List<int>
}

ListOfInts reverseListOfNumbers(ListOfInts list){
	var reversed = list.reversed;
	return reversed.toList();
}

```

# Q&A

**Q. SDK란 무엇입니까?**
A. 개발자가 소프트웨어를 만들기 위해 필요한 도구들과 라이브러리, 문서, 예제 코드 등이 포함되는 도구 모음이며, 이를 통해 개발자는 소프트웨어 개발을 보다 쉽고 빠르게 할 수 있습니다. 특정 플랫폼이나 프로그래밍 언어에 제공됩니다. Android SDK는 안드로이드 애플리케이션을 개발하기 위한 도구 모음이며, iOS SDK는 iOS 애플리케이션을 개발하기 위한 도구 모음입니다.

**Q. 코드베이스란 무엇입니까?**
A. 프로그램의 기능을 유지하거나, 소스 코드의 구현을 유지하는 데에 필요한 완전한 소스 코드를 뜻합니다.

**Q. 바이너리의 정확한 의미가 무엇입니까?**
A. 다트에 대한 개념까진 다루기 힘들고, 플러터의 경우에는 바이너리로 컴파일이 되고, 바이너리 파일이 어딘가에 있겠지만 실제로 접할 일이 거의 없습니다.

**Q. zshrc가 무슨 파일인지 궁금합니다. 항상 환경변수 설정할 때 그냥 설명 따라서 파이 설정했는데 왜 하는 건지 모르겠습니다..!**
A.

```
export PATH="$PATH:`pwd`/flutter/bin"
```

이렇게 하면 일회성으로만 현재 터미널 창에 대해서 플러터 도구를 path에 추가할 수 있는데요,
zshrc 파일에 작성하면, zshrc 파일이 수정되지 않는 이상 플러터의 경로를 path에 영구적으로 설정할 수 있습니다.
