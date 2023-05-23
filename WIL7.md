# WIL7

Created by: 고여경
Created time: 2023년 5월 23일 오후 4:05
Last edited by: 고여경
Last edited time: 2023년 5월 24일 오전 12:35

Week7 과제 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/af355910-d7a5-45da-8440-76c5851914e3/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/88e39ce1-55b6-4be0-9881-3f47ab4751b6/Untitled.png)

## SafeArea()

핸드폰마다 카메라, 버튼의 위치가 제각각이라 기종에 따라 내용이 가려지거나 사라지는 UI가 있을 수 있다. 원하는 위젯을 SafeArea로 감싸주면 된다.

---

## ListView()

스크롤을 구현하기 위해 가장 기본적으로 사용하는 위젯이다. 

+ListView.builder()

속성으로 itemCount, itemBuilder가 들어간다. itemCount만큼 itembuilder를 실행시켜 widget을 반환한다. 반환한 widget들이 쌓여 ListView를 생성하게 된다. 리스트값을 넣을 때 보통 쓴다. ex. ${list[index]}

+ListView.separated()

각 요소 사이에 다른 요소를 넣게 해주는 방법이다. 보통 ListView 각 요소 사이에 Divider(구분선)를 넣을 때 사용한다.

---

## GridView.builder()

listView와 유사하지만 gridView는 타일뷰 형태다. GridView는 5개의 Constructor들이 있는데 그 중 builder를 주로 사용한다. 

```dart
GridView.builder(
              primary: false,
              shrinkWrap: true,
              itemCount: keywords.length, //item 개수
              gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 3, //하나의 행에 보여줄 아이템의 개수
                childAspectRatio: 103 / 64, //아이템의 가로, 세로 비율
                mainAxisSpacing: 9, // 수평 빈 공간
                crossAxisSpacing: 8, //수직 빈 공간
              ),
              itemBuilder: (context, index) {//item의 반복문 항목 형
                return Container(
                  decoration: BoxDecoration(
                      ...
                  child: Center(
                    child: Text(
                      '${keywords[index]}',
                      style: TextStyle(
                        ...
                      ),
                    ),
                  ),
                );
              })
        ],
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bbfc4006-82f1-49eb-894b-fe4a5e6ee18e/Untitled.png)

---

## Wrap widget

줄과 행에서 공간이 부족하면 알아서 다음 줄로 넘어감. 줄과 행처럼 자식을 한 줄에 배치함. 

buttons과 chips을 나열할 때 유용하다.

```dart
const Wrap(
              spacing: 4.0,
              runSpacing: 6.0,
              children: [
                KeywordBox(
                  keyword: "우유부단",
                ),
								KeywordBox(),
								...
```

KeywordBox를 가로로 두는 코드다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d06250bb-dd21-4fee-8306-1d26fa8b5daa/Untitled.png)

---

## AspectRatio 위젯

앱을 배치할 때 실제 크기에 관계없이 위젯이 특정한 넓이를 가지도록 원할 때 사용한다. ClipRRect 하위에 둔다. image 위에 감싸면 됨

`aspectRatio` : 3/2 이렇게도 됨. 너비 세 부분 높이 2부분 = 1.5로 한다는거

하위 요소로는 container, image다 됨. 

+Expanded 아래에 들어가면 안됨. 무시당해. 

```dart
child: ClipRRect(//사진 둥글게
                    borderRadius: BorderRadius.circular(10),
                    child: AspectRatio(
                        //image 가로세로 비율 맞춰줌
                        aspectRatio: 1,
                        child: Image.asset(
                          "assets/images/${images[index]}",
                          fit: BoxFit.cover,
                        )),
                  ),
```
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/11276fa5-43c1-4ea7-ab07-1c4bba328cea/Untitled.png)

---

## AppBar :

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f47be4f-fafa-4538-b2b7-e644bfb51d3b/Untitled.png)

```dart
appBar: AppBar(
        // TODO 쓰인 AppBar의 속성들에 대해 조사해 보세요.
        backgroundColor: const Color(0xFFF8F8F8),
        bottom: PreferredSize(
          preferredSize: const Size.fromHeight(1.0),
          child: Container(
            color: const Color(0xFFECECEC),
            height: 1.0,
          ),
        ),
        elevation: 0.0,
        centerTitle: true,
        iconTheme: const IconThemeData(
          color: Color.fromARGB(255, 61, 20, 20),
        ),
        leading: IconButton(
          onPressed: () {
            Navigator.pop(context);
          },
          icon: const Icon(Icons.arrow_back_ios, size: 16),
        ),
        title: const Text(
          "웰시코기 캐해 작성",
          style: TextStyle(
            ...
          ),
        ),
      ),
```

todo에 쓰인 속성들 위주

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/08f2b85c-5cb6-4a4e-9803-17919e939ec8/Untitled.png)

- bottom : PreferredSize는 appbar의 hight 기본에서 추가 변경시킬 수 있다.
- elevation : 그림자 정도 변경. 0으로 하면 그림자x
- leading : 맨 좌측 아이콘 넣을 수 있음.
- iconTheme :  뒤로가기 버튼 색을 변경하기위해 사용하는 속성.

---

## ‘지인들의 캐해 짤’을 선택했을 때 image를 크게 보고 싶을 때

1. 사진마다 클릭이 가능해야하고,
2. 클릭했을 때의 해당 사진만 전체 화면에 보여야한다.
3. 사진만 보여주는 코드를 작성해 클릭 시에 그 코드 화면으로 이동한다고 생각하면 된다.

우선 image_page.dart를 생성한다.

```dart
//image_page.dart
class ImagePage extends StatelessWidget {
  const ImagePage({
    super.key,
    required this.imageUrl,
  });

  final String imageUrl;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
          child: ListView(
        children: [
          Image.asset("assets/images/$imageUrl"),
        ],
      )),
    );
  }
}
```

각각의 사진를 imageUrl 변수로 생각한다. 클릭에 따라 imageUrl을 인자로 받아올거다.

`fianl String imageUrl`로 변수 설정해주고, `required this.imageUrl`로 받아올 인자를 설정해준다.

```dart
//home_page.dart
GridView.builder(
...
	return GestureDetector(
                  onTap: () {
                    Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => ImagePage(
                            imageUrl: images[index],
                          ),
                        ));
                  },
                  child: ClipRRect(
                    //사진 둥글게
                    borderRadius: BorderRadius.circular(10),
                    child: AspectRatio(
										...
```

클릭할 화면인 home_page.dart에서 클릭을 탐지하는 위젯 `GestureDetector`을 사진에 해당되는 `ClipRRect`위젯 위에 추가한다. 

그리고 GestureDetector 속성으로 `onTap(){}` 을 넣어 클릭 시에 무슨 행동을 할지 정해준다. 

Navigator.push 를 이용해 화면 이동한다. 

## MaterialPageRoute

1. router 개념 : 하나의 페이지나 화면
2. Navigator : 모든 앱 페이지를 스택 자료 구조로 route 객체를 관리하고 있는 기능 →(push : 이동할 화면 추가. pop : 이전 화면으로 이동하기 가능)
3. MaterialPageroute 위젯과 context :
- return하는 모든 scaffold와 같은 위젯이 router라고 볼 수 있다. context를 이용해 위치 정보를 쌓아 올리기 위해 사용. 최초 페이지의 위치를 알기 위해 context를 사용한다.
1. MaterialPageRoute는 flutter가 기본으로 제공하는 기능으로 builder를 제공하며 라우팅을 하는 과정에서 안전장치로 사용한다. 앱상에서 페이지 이동을 할 때 기본 에니메이션이 제공된다. android는 fade in/fade out이 적용되고 ios에서는 좌우로 움직이면서 페이지가 이동된다.
