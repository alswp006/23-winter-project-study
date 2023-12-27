**List,Set,map 의 형변환 방법**

```dart
void main() {
  List<String> blackMinjae = ['로제','지수','리사','제니','제니'];
  
  print(blackMinjae);
  print(blackMinjae.asMap()); //맵으로 변환 해주는 메소드 리스트에서 제공해줌
  print(blackMinjae.toSet()); //셋으로 변환 해주는 메소드 중복 제거 자동으로

  Map blackMinjaeMap = blackMinjae.asMap();
  
  print(blackMinjaeMap.keys);
  print(blackMinjaeMap.values);
  
  Set blackMinjaeSet = Set.from(blackMinjae); //리스트로 부터 셋을 만드는 방법
  
  print(blackMinjaeSet.toList()); //셋을 리스트로 만드는 방법

}
```

**매핑이란? 하나의 형태에서 또 다른 형태로 만들어 내는것**! 

**List를 매핑 하는 방법!**

**Map: 맵을 쓰면 새로운 리스트가 계속 생성된다.!!!**

```dart
void main() {
  List<String> blackMinjae = ['로제','지수','리사','제니'];
  
  final newBlackMinjae = blackMinjae.map((x){
    return '블랙핑크 $x'; 
    
  }); //메핑 방법 x값에 위 리스트 값이 들어간다 새로운 리스트 생성!! 
 
  print(blackMinjae);
  print(newBlackMinjae); //멤버들 이름 앞에 블랙핑크가 붙은채로 나옴
  print(newBlackMinjae.toList()); //List 형태로 변환
  
  //맵을 사용하면 하나의 형태에서 또다른 형태로 변경할 수 있다.
  
  final newBlackMinjae2 = blackMinjae.map((x) => '블랙핑크 $x'); 
  // 에로우 사용 위랑 같음 
  
  
  
  String number ='13579';
  
  final parsed = number.split(''); //split 스트링 값들을 하나의 글자들로 나타내어줌
  // 1,3,5,7,9
  print(parsed);

	}
```

**Map을 매핑 하는 방법**

```dart
void main() {
  Map<String, String> harryPotter = {
    'Harry Potter' : '해리 포터',
    'Ron Weasley' : '론 위즐리',
    'Hermione Granger' : '헤르미온느 그레인저'    
  };
  
  
  final result = harryPotter.map(
  (key, value) => MapEntry( //MapEntry클래스를 이용하여 매핑 한다.
        'Harry Potter Character $key',
        '해리포터 캐릭터 $value',
  )
  );
  print(result);
  
  final keys = harryPotter.keys.map((x) => 'HPC $x').toList(); // 키 값들을 List로 메핑
  final values = harryPotter.values.map((x) => '해리포터 $x').toList(); // value 값들을 List로 메핑
  print(keys);
  print(values);
  
}
```

**Set을 메핑 하는 방법**

```dart
void main() {
  Set blackPinkSet = {
    '로제',
    '제니',
    '지수',
    '리사',
  };
  
  final newSet = blackPinkSet.map((x) => '블랙핑크 $x').toSet(); // Set으로 메핑
  print(newSet);
}
```

**Where: 일종의 필터링을 해준다** 

```dart
void main() {
 List<Map<String,String>> people = [ //리스트 안에 map을 넣을 수 있다.
   {
     'name': '로제',
     'group': '블랙핑크',
   },
   {
     'name': '지수',
     'group': '블랙핑크',
   },
   {
     'name': 'RM',
     'group': 'BTS',
   },
   {
     'name': '뷔',
     'group': 'BTS',
   },
 ];
  
  print(people);
  
  final blackPink = people.where((x) => x['group'] == '블랙핑크');
  print(blackPink); // 블랙핑크 값만 찾아서 출력해준다
}
```

**reduce 사용 코드**

```dart
void main() {
  List<int> numbers = [
    1,
    3,
    5,
    7,
    9
  ];
  
  final result = numbers.reduce((prev, next){
    print('-----------------');
    print('previous : $prev');
    print('next : $next');
    print('total : ${prev +next}');
    
    return prev + next;
  });
  
  print(result);
   // prev에는 맨 처음값만 들어가고 이후 next에는 다음 아이템 값이 들어간다.
  
  List<String> words = [
    '안녕하세요 ',
    '저는 ',
    '이정환입니다.',
  ];
  
  final sentence = words.reduce((prev, next) => prev + next);
  print(sentence);
  // reduce는 꼭 reduce를 실행하는 리스트와 같은 타입만 실행할 수 있다!!!!
}
```

**fold: reduce에서 같은 타입만 실행할 수 있는걸 해결할 수 있다.**

```dart
void main() {
  List<int> numbers = [1,3,5,7,9];
  
  final sum = numbers.fold<int>(0,(prev, next) => prev +next);
  //대신 시작 값을 정해주어야 한다 0
  print(sum);
  
  List<String> words = [
    '안녕하세요 ',
    '저는 ' ,
    '이정환 입니다.',
  ];
  
  final sentence = words.fold<String> ('',(prev,next) => prev + next);
  print(sentence);
  
  final count = words.fold<int>(0, (prev, next) => prev + next.length);
  print(count); //이렇게 List에 있는 타입과 달라도 출력할 수 있다.
  

}
```

**cascading operator: 여러개의 리스트드를 합칠 때**

```dart
void main() {
  List<int> even = [
    2,
    4,
    6,
    8,
  ];
  
  List<int> odd = [
    1,
    3,
    5,
    7,
  ];
 
//cascading operator
// ...  을 이용해서 사용 리스트안에 리스트가 생기는 것이 아닌 리스트가 합쳐짐
  
  print([...even, ...odd]); //...을 사용하면 새로운 리스트가 생기는 것이다.
  
}
```
