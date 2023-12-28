## Future 키워드

```dart
void main() {
  // Future - 미래
  // 미래에 받아올 값
  
  Future<String> name = Future.value('이정환');
  Future<int> number = Future.value(1);
  Future<bool> isTrue = Future.value(true);
  
  print("함수 시작");
  
  // 2개의 파라미터
  // delayed - 지연되다.
  // 1번 파라미터 - 지연할 시간 (얼마나 지연할건지) duration
  // 2번 파라미터 - 지연 시간이 지난 후 실행할 함수.
  
  Future.delayed(Duration(seconds: 2), () {
    print("Delay 끝");
  });

}
```

## Future 키워드2

```dart
void main() {
  // Future - 미래
  // 미래에 받아올 값
  
  Future<String> name = Future.value('이정환');
  Future<int> number = Future.value(1);
  Future<bool> isTrue = Future.value(true);
  
  addNumbers(1, 1);
}

void addNumbers(int number1 , int number2) {
  print('계산 시작: $number1 + $number2');
  
  //서버 시뮬레이션
  Future.delayed(Duration(seconds: 2), () {
    print('계산 완료: $number1 + $number2 = ${number1 + number2}');
    
  }); // duration 을 이용하여 출력 순서가 바뀌었다.. 2초간 기다리고 다른 코드를 실행
  // 그후 2초후 duration함수를 실행
  
  print('함수 완료');
}
```

## await 키워드

함수 파라미터 와 바디({}) 옆에 async를 입력 한다 await는 duration이 실행되기 전까지 밑에 코드를 실행하지 않는다 하지만 cpu는 그 시간에 노는게 아닌 addNumbers(2,2)를 또 실행한다. 

```dart
void main() {
  // Future - 미래
  // 미래에 받아올 값
  
  Future<String> name = Future.value('이정환');
  Future<int> number = Future.value(1);
  Future<bool> isTrue = Future.value(true);
  
  addNumbers(1, 1);
  addNumbers(2, 2);
}

void addNumbers(int number1 , int number2) async {
  print('계산 시작: $number1 + $number2');
  
  //서버 시뮬레이션
  await Future.delayed(Duration(seconds: 2), () {
    print('계산 완료: $number1 + $number2 = ${number1 + number2}');
    
  }); 
  
  print('함수 완료 :  $number1 + $number2');
}
```

- await는 future키워드를 return해주는 함수에만 사용할 수 있다!

```dart
void main() async {
  // Future - 미래
  // 미래에 받아올 값
  
  Future<String> name = Future.value('이정환');
  Future<int> number = Future.value(1);
  Future<bool> isTrue = Future.value(true);
  
  await addNumbers(1, 1); // await는 future키워드를 return해주는 함수에만 사용할 수 있다!
  await addNumbers(2, 2); // await는 future키워드를 return해주는 함수에만 사용할 수 있다!
   
    // 이렇게 async와 await를 사용하면 addNumber(1,1) 함수가
    // 실행이 다 되고 나서 addNumber(2,2)함수가 실행이 된다.
}

Future<void> addNumbers(int number1 , int number2) async {
  print('계산 시작: $number1 + $number2');
  
  //서버 시뮬레이션
  await Future.delayed(Duration(seconds: 2), () {
    print('계산 완료: $number1 + $number2 = ${number1 + number2}');
    
  }); 
  
  print('함수 완료 :  $number1 + $number2');
}
```

- async를 이용해서 return값을 받는 것 도 가능하다!!

```dart
void main() async {
  // Future - 미래
  // 미래에 받아올 값
  
  Future<String> name = Future.value('이정환');
  Future<int> number = Future.value(1);
  Future<bool> isTrue = Future.value(true);
  
 final result1 = await addNumbers(1, 1);
 final result2 = await addNumbers(2, 2);
   
 
}

Future<int> addNumbers(int number1 , int number2) async {
  print('계산 시작: $number1 + $number2');
  
  //서버 시뮬레이션
  await Future.delayed(Duration(seconds: 2), () {
    print('계산 완료: $number1 + $number2 = ${number1 + number2}');
    
  }); 
  
  print('함수 완료 :  $number1 + $number2');
  
  return number1 + number2; //리턴값을 반환해줄 수도 있다!
}
```

## Stream 키워드

future는 하나의 데이터를(결과값) 전달 받지만 stream은 연속된 데이터를 listen()을 통해서 비동기적으로 처리할 수 있다. 예를 들면 실시간으로 데이터를 처리할 때 future는 이미지 파일 하나를 다운로드 하여 보여줄 때 적합하다면 stream은 동영상(연속된 이미지)를 보여주는데 사용할 수 있다. 흔히 말하는 streaming 서비스의 동작 방식

```dart
import 'dart:async';

void main() {
  final controller = StreamController();
  final stream = controller.stream;
  
  final streamListner1 = stream.listen((val) {
    print('Listener 1 : $val'); //하나의 함수를 받아야함
  });
  
  controller.sink.add(1);
  controller.sink.add(2);
  controller.sink.add(3);
  controller.sink.add(4);
  controller.sink.add(5);
  
}
```

## Stream 키워드 2

```dart
import 'dart:async';

void main() {
  final controller = StreamController();
  final stream = controller.stream.asBroadcastStream();
  //asBroadcastStream을 사용하면 listen함수를 여러 번 사용할 수 있다.
  
  final streamListner1 = stream.where((val) => val %2 == 0).listen((val){
 // 이렇게 함수를 이용해 데이터를 다룰 수 있다.
    print('Listener 1 : $val'); //하나의 함수를 받아야함
  });
   final streamListner2 = stream.where((val) => val %2 == 1).listen((val){
    print('Listener 1 : $val'); //하나의 함수를 받아야함
  });
  
  controller.sink.add(1);
  controller.sink.add(2);
  controller.sink.add(3);
  controller.sink.add(4);
  controller.sink.add(5);
  
  
}
```

## Stream 을 이용한 비동기식 프로그래밍

```dart
import 'dart:async';

void main() {
  calculate(2).listen((val) {
    print('calculate(2) : $val');
  });
  
    calculate(4).listen((val) {
    print('calculate(4) : $val');
  });
  
  
 
}

Stream<int> calculate(int number) async* { //future를 쓸 때 처럼 async*을 return대신 yield를 
사용하면 된다.
  for(int i = 0; i < 5; i++) {
    yield i *number;
    
    await Future.delayed(Duration(seconds: 1));
  }
}
```

Stream도 future처럼 await할 수 있는 방법이 있다.

```dart
import 'dart:async';

void main() {
  playAllStream().listen((val) {
    print(val);
  });
 
}

Stream<int> playAllStream() async* {
  yield* calculate(1);
  yield* calculate(1000);
}

Stream<int> calculate(int number) async* {
  for(int i = 0; i < 5; i++) {
    yield i *number;
    
    await Future.delayed(Duration(seconds: 1));
  }
}
```
