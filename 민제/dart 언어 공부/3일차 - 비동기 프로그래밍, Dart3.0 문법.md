## 비동기 프로그래밍

- 쓰레드 : 컴퓨터가 작업하는 가장 작은 단위

### Synchronous Programming

- Cpu가 작업하는 동안은 다른 작업을 할 수 없다.
    - 이는 서버 요청이 들어가는 순간 문제가 발생한다.\
    - Cpu가 작업하는 동안 서버 요청이 들어오면 Cpu는 놀게 된다.

### Asynchronous Programming

- 작업 중에도 다른 작업을 수행할 수 있다.
- 즉 특정 코드의 처리가 완료되기 전, 처리하는 도중에도 아래로 계속 내려가며 수행을 하는 것이다.
- 각각의 Cpu쓰레드를 사용하는데 효율적이다.
- delayed
    
    ```dart
    void main() {
      //미래에 받아올 값
      Future<String> name = Future.value("kimminje");
      
      //delayed : 지연
      //1번째 파라미터 : 지연할 기간
      //2번째 파라미터 : 지연 기간이 지난 후 실행할 코드
      Future.delayed(Duration(seconds : 2), (){
        print("Delay 끝");
      });
    }
    ```
    
    - 함수
    - Future를 쓰면 async prog가 가능하기 때문에 딜레이되는 동안 다른 코드를 실행하고 시간이 되면 돌아옴
    
    ```dart
    void main() {
      //미래에 받아올 값
      Future<String> name = Future.value("kimminje");
      
      addNumber(1,1);
    }
    
    void addNumber(int num1, int num2){
      print("계산 시작");
      
      Future.delayed(Duration(seconds : 2), (){
        print("계산 완료 $num1 + $num2 = ${num1+num2}");
      });
      
      print("함수 완료");
    }
    //출력
    계산 시작
    함수 완료
    계산 완료 1 + 1 = 2
    ```
    
    - 여러번 메소드를 실행해도 똑같이 cpu는 쉬지않고 일한다.
    
    ```dart
    void main() {
      //미래에 받아올 값
      Future<String> name = Future.value("kimminje");
      
      addNumber(1,1);
      addNumber(2,2);
    }
    
    void addNumber(int num1, int num2){
      print("계산 시작");
      
      Future.delayed(Duration(seconds : 2), (){
        print("계산 완료 $num1 + $num2 = ${num1+num2}");
      });
      
      print("함수 완료");
    }
    //출력
    계산 시작
    함수 완료
    계산 시작
    함수 완료
    계산 완료 1 + 1 = 2
    계산 완료 2 + 2 = 4
    ```
    
- await : 인터럽트같은 느낌
    
    ```dart
    void main() {
      //미래에 받아올 값
      Future<String> name = Future.value("kimminje");
      
      addNumber(1,1);
      addNumber(2,2);
    }
    
    void addNumber(int num1, int num2) async { //Future같은 async함수앞에 await 삽입 가능
      print("계산 시작");
      
      await Future.delayed(Duration(seconds : 2), (){
        print("계산 완료 $num1 + $num2 = ${num1+num2}");
      });
      
      print("함수 완료 $num1");
    }
    //출력
    계산 시작
    계산 시작
    계산 완료 1 + 1 = 2
    함수 완료 1
    계산 완료 2 + 2 = 4
    함수 완료 2
    ```
    
    ```dart
    void main() async {
      //미래에 받아올 값
      Future<String> name = Future.value("kimminje");
      
      await addNumber(1,1);
      await addNumber(2,2);
    }
    
    Future<void> addNumber(int num1, int num2) async { //Future같은 async함수앞에 await 삽입 가능
      print("계산 시작");
      
      await Future.delayed(Duration(seconds : 2), (){
        print("계산 완료 $num1 + $num2 = ${num1+num2}");
      });
      
      print("함수 완료 $num1");
    }
    //출력
    계산 시작
    계산 완료 1 + 1 = 2
    함수 완료 1
    계산 시작
    계산 완료 2 + 2 = 4
    함수 완료 2
    ```
    

### Stream

- 함수가 실행되면 완료될 때까지 여러 값을 반환받을 수 있다.
    
    ```dart
    import "dart:async";
    
    void main() {
      final controller = StreamController();
      final stream = controller.stream;
      
      final streamListener1 = stream.listen((val){
        print("Listener1 : ${val}");
      });
      
      controller.sink.add(1);
      controller.sink.add(2);
      controller.sink.add(3);
      controller.sink.add(4);
      controller.sink.add(5);
    }
    //출력
    Listener1 : 1
    Listener1 : 2
    Listener1 : 3
    Listener1 : 4
    Listener1 : 5
    ```
    
- 여러 스트림 받기
    
    ```dart
    import "dart:async";
    
    void main() {
      final controller = StreamController();
      final stream = controller.stream.asBroadcastStream();
      
      final streamListener1 = stream.listen((val){
        print("Listener1 : ${val}");
      });
      final streamListener2 = stream.listen((val){
        print("Listener2 : ${val}");
      });
      
      controller.sink.add(1);
      controller.sink.add(2);
      controller.sink.add(3);
      controller.sink.add(4);
    }
    //출력
    Listener1 : 1
    Listener2 : 1
    Listener1 : 2
    Listener2 : 2
    Listener1 : 3
    Listener2 : 3
    Listener1 : 4
    Listener2 : 4
    ```
    
- 스트림에 조건 주기
    
    ```dart
    import "dart:async";
    
    void main() {
      final controller = StreamController();
      final stream = controller.stream.asBroadcastStream();
      
      final streamListener1 = stream.where((val) => val%2==0).listen((val){
        print("Listener1 : ${val}");
      });
      final streamListener2 = stream.where((val) => val%2!=0).listen((val){
        print("Listener2 : ${val}");
      });
      
      controller.sink.add(1);
      controller.sink.add(2);
      controller.sink.add(3);
      controller.sink.add(4);
    }
    //출력
    Listener2 : 1
    Listener1 : 2
    Listener2 : 3
    Listener1 : 4
    ```
    
- yield : 여러 개 반환
    
    ```dart
    import "dart:async";
    
    void main() {
      calculate(1).listen((val){
        print("calculate : $val");
      });
    }
    
    Stream<int> calculate(int num) async* {
      for (int i = 0; i<5; i++){
        yield i*num;
      }
    }
    //출력
    calculate : 0
    calculate : 1
    calculate : 2
    calculate : 3
    calculate : 4
    ```
    
    - 메소드 2개 동시 실행
        
        ```dart
        import "dart:async";
        
        void main() {
          calculate(1).listen((val){
            print("calculate1 : $val");
          });
          
          calculate(2).listen((val){
            print("calculate2 : $val");
          });
        }
        
        Stream<int> calculate(int num) async* {
          for (int i = 0; i<5; i++){
            yield i*num;
            
            await Future.delayed(Duration(seconds:1));
          }
        }
        //출력
        calculate1 : 0
        calculate2 : 0
        calculate1 : 1
        calculate2 : 2
        calculate1 : 2
        calculate2 : 4
        calculate1 : 3
        calculate2 : 6
        calculate1 : 4
        calculate2 : 8
        ```
        
        - 한 메소드가 끝나고 나서 실행
        
        ```dart
        import "dart:async";
        
        void main() {
          playAllStream().listen((val){
            print(val);
          });
        }
        
        Stream<int> playAllStream() async* {
          yield* calculate(1);
          yield* calculate(1000);
        }
        
        Stream<int> calculate(int num) async* {
          for (int i = 0; i<5; i++){
            yield i*num;
            
            await Future.delayed(Duration(seconds:1));
          }
        }
        //출력
        0
        1
        2
        3
        4
        0
        1000
        2000
        3000
        4000
        ```
        

## Dart 3.0 업데이트 문법

- record : list규격화 (~=파이썬의 tuple)
- 타입의 순서를 보장함
    
    ```dart
    void main() {
      final listResult = lNameAndAge({
        'name' : 'kimminje',
        'age' : 26
      });
      
      final tupleResult = rNameAndAge({
        'name' : 'kimminje',
        'age' : 26
      });
      
      print(listResult[0]);
      print(tupleResult.$1);
    }
    
    lNameAndAge(Map<String, dynamic> json){
      return [json['name'], json['age']];
    }
    
    (String, int) rNameAndAge(Map<String, dynamic> json){
      return (json['name'] as String, json['age'] as int);
    }
    ```
    
- 활용
    
    ```dart
    void main(){
      final names = rNameAndAge();
      
      for (final name in names) {
        print(name.$1);
        print(name.$2);
      }
      
      final names2 = namedNameAndAge();
      
      for (final name in names2) {
        print(name.name);
        print(name.age);
      }
    }
    
    List<(String name, int age)> rNameAndAge(){
      return [
        ('민제', 26),
        ('정환', 25)
      ];
    }
    
    List<({String name, int age})> namedNameAndAge(){
      return [
        (name : '민제', age : 26),
        (name : '정환', age : 25)
      ];
    }
    ```
    
- destructuring
    
    ```dart
    void main(){
      final (name, age) = ('민제', 26);
     
      final names = ['민제', 26];
      final [name1, age1] = names;
      
      final numbers = [1,2,3,4,5,6];
      final [x, y, ..., z] = numbers;
      print(x);
      print(y);
      print(z);
      
      final [xx, yy, ...rest, zz] = numbers;
      print(rest);
      
      final [xxx, _, yyy, ...rest2, zzz, _] = numbers;
      print(xxx);
      print(yyy);
      print(zzz);
      print(rest2);
      
      final minje = {'name' : '민제', 'age' : 26};
      final {'name' : name2, 'age' : age2} = minje;
    }
    //출력
    1
    2
    6
    [3, 4, 5]
    1
    3
    5
    [4]
    ```
    
- 다양한 switch 사용
    
    ```dart
    void main(){
      switcher([1,2,3]);
      switcher([1,2]);
      switcher(7);
      switcher(17);
    }
    
    void switcher(dynamic anything){
      switch(anything){
        case [_, _, _]:
          print("match : [_,_,_]");
        case [int a, int b]:
          print("match : int $a int $b");
        case <10 && >5:
          print("match : <10 && >5");
        default:
          print('no match');
      }
    }
    //출력
    match : [_,_,_]
    match : int 1 int 2
    match : <10 && >5
    no match
    ```
    
- matcher
    
    ```dart
    void main(){
      matcher();
    }
    
    void matcher(){
      final members = {{'name' : 'kim', 'age' : 26},{'name' : 'lee', 'age' : 25}};
      
      for (var {'name' : name, 'age' : age} in members){
        print(name);
        print(age);
      }
      
      final minje = {'name' : 'kim', 'age' : 26};
      if (minje case {'name' : String name, 'age' : int age}){
        print(name);
        print(age);
      }
    }
    //출력
    kim
    26
    lee
    25
    kim
    26
    ```
    
- final class는 상속, 구현, mixin 사용 불가
- base class는 상속은 가능하지만 구현은 불가능하다
- interface class는 구현만 가능하다.
- sealed class는 abstract하면서 final이고 패턴매칭을 사용할 수 있게 해준다.
- mixin class는 extends나 with를 사용할 수 없다.
- 클래스는 on 키워드를 사용할 수 없다.
