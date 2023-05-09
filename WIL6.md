# WIL6

Created by: 고여경
Created time: 2023년 5월 6일 오전 12:37
Last edited by: 고여경
Last edited time: 2023년 5월 10일 오전 12:25

# EventLeSSARAFIM
![Untitled](https://github.com/yeogaeng/GDSC-OC-MOBILE-WIL/assets/81527268/8784b2d0-cfcf-4bce-b7ab-15c1af2c748a)
해당되는 코드를 ctrl+shift+R 눌러서 extract Method로 해당되는 부분을 ‘EventLeSSARAFIM’ 위젯으로 빼줬다.

- ClipRReect 로 Image.asset(’이미지 경로’)를 묶으면 사진 border를 수정할 수 있다.
- Stack은 사진 위에 Text 올리기 위해서 사용한다. alignment로 글자 위치 이동한다. ClipRRect를 Stack이 감싸고있다.

새롭게 알게 된 코드

```dart
**Stack(
        alignment: Alignment.bottomLeft,
        children: [
          ClipRRect(
              borderRadius: BorderRadius.circular(12.0),
              child: Image.asset('assets/images/le.png'))**,
...
```

전체 코드

```dart
class EventLeSSERAFIM extends StatelessWidget {
  const EventLeSSERAFIM({
    super.key,
  });

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.symmetric(horizontal: 20.0),
      child: **Stack(
        alignment: Alignment.bottomLeft,
        children: [
          ClipRRect(
              borderRadius: BorderRadius.circular(12.0),
              child: Image.asset('assets/images/le.png'))**,
          Padding(
            padding: const EdgeInsets.only(left: 12),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(
                  'EVENT',
                  style: TextStyle(color: WHITE, fontSize: 19),
                ),
                Text(
                  'LE SSERAFIM',
                  style: TextStyle(
                      color: WHITE, fontWeight: FontWeight.w900, fontSize: 23),
                ),
                Text(
                  '지금 이벤트 참가하고 르세라핌 굿즈 받기',
                  style: TextStyle(color: WHITE, fontSize: 13),
                ),
                const SizedBox(
                  height: 38,
                )
              ],
            ),
          )
        ],
      ),
    );
  }
}
```

# 추가로 알게된 점

- 빈칸은 sizedbox로
- Container 늘리기 width: double.infinity로 둔 다음에 양옆 20으로 margin
padding : symmetric 으로 두고 horizon, vertical로 변화줌
- arrow_forward
- arrow_forward_ios

### flutter 추천 작업 띄워주는 단축키

-ctrl+shift+R (= ctrl+.)

-ctrl+space 

SingleChildScrollView로 overflow없이 스크롤되게 화면밖으로 넘어가게함
scrollDirection = Axis.horizon

# 최근 등록된 심부름
![Untitled 1](https://github.com/yeogaeng/GDSC-OC-MOBILE-WIL/assets/81527268/672a0ea8-a18d-403e-a5e0-875d0e92fe82)
최근 등록된 심부름 위젯 재사용 

-> 공통widget으로 만들어서 변경되는 값은 인자값으로 넣어줌

```dart
class NewSimbooreumContainer extends StatelessWidget {
  const NewSimbooreumContainer(
      {super.key,
      required this.boxColor,
      required this.textColor,
      required this.title,
      required this.isNeedMore});

  @override
  final Color boxColor;
  final Color textColor;
  final String title;
  final bool isNeedMore;

	...
```

인자값을 넣어주기위해 class 생성자에 받는 인자값이 Null이 안되게 required로 선언해주고 @override 아래에 class마다 바뀌는 요소들을 변수로 만들어준다.

+2 동그라미 박스(isNeedMore)는 bool값으로 해준다. 

```dart
isNeedMore
                      ? Padding(
                          padding: const EdgeInsets.only(left: 8.0),
                          child: Container(
                            decoration: BoxDecoration(
                              shape: BoxShape.circle,
                              color: PRIMARY_COLOR,
                            ),
                            child: Padding(
                              padding: const EdgeInsets.all(5.0),
                              child: Text(
                                '+2',
                                style: TextStyle(fontSize: 12, color: WHITE),
                              ),
                            ),
                          ),
                        )
                      : SizedBox.shrink()
```

이렇게 

`isNeedMore?(참일 때 수행하는 코드):(거짓일때 사용하는 코드)`

---

아무것도 출력하고싶지 않다면

`isNeedMore? Widget : Sizedbox.shrink` 

Sizedbox.shrink 사용!!!!

---

# 최근등록된 후기

-사진은 위에만 둥글고 아래는 뾰족하게 하면 ClipRRect로 감싸고, bordercircular를 topLeft, topright로만 바꿔줌

-ctrl+shift+R로 ExtractWidget눌러 그냥 container도 이름붙여서 바꿔줌.(사실 위젯을 밖으로 빼내준것)
![Untitled 2](https://github.com/yeogaeng/GDSC-OC-MOBILE-WIL/assets/81527268/fb1f1f25-cafb-4f27-b22d-7d9b11570f34)


1. 이미지 윗부분만 둥근 모서리 주기

 위쪽만 모서리를 둥글게 만들고 싶을 때는 `ClipRRect`를 써서, `borderRadius : BorderRadius.only()`를 사용하고, 괄호안에 `topLeft, topRight`값에 `Radius.circular(14)` 로 적어주면된다. 자동완성을 이용해서 찾아보자.

1. 이미지 확대되게 꽉 채우기

 `fit: BoxFit.cover` : 비율을 유지한채 지정영역을 꽉 채운다.

참고한 블로그 (BoxFit) : [https://devmg.tistory.com/181](https://devmg.tistory.com/181)

[code]

```dart
ClipRRect(
                borderRadius: BorderRadius.only(
                    topLeft: Radius.circular(14),
                    topRight: Radius.circular(14)), //위쪽만 모서리를 둥글게 만들고 싶을 때, 이렇게 하면됨.
                child: Container(
                  height: 70,
                  width: 140,
                  decoration: BoxDecoration(color: GREEN300),
                  child: Image.asset(
                    'assets/images/le_chae.jpg',
                    fit: BoxFit.cover,
                  ),
                ),
              ),
```

# Q&A

Q. stless 위젯 만들면 자동으로 뜨는 super.key, @override이 어디에 사용되는건지 궁금합니다. super.key는 지우면 안되는건가요? 

Q. Extract widget과 Extract method 차이가 무엇인가요?
