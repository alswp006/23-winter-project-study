1.변수
void main() {
 // variable(변수)
  
  var name = '코드팩토리'; // 변수 선언은 var (변수이름)
  
  print (name); //출력은 print
  
  var name2 ='레드벨벳';
  
  print (name2);
  
  name = '플러터 프로그래밍'; //변수의 값 바꾸기 , 똑같은 이름의 변수선언은 불가능
  
  print (name);  
}

void main() {
 // 정수는 integer
  
  int number1 = 10; //정수 10 '10'은 문자열 10 따로 봄
  
  print(number1);
  
  int number2 = 15;
  print(number2);
  
  int number3 = -20;
  print(number3);
  
}

void main() {
 // 정수
 // integer
  
  int number1 = 2;
  int number2 = 4;
  
  print(number1 + number2);  // 플러터의 사칙연산들
  print(number1 - number2); 
  print(number1 / number2);
  print(number1 * number2);
  
}

void main() {
  //실수
  //double
  double number1 = 2.5;
  double number2 = 0.5;
}

void main() {
  //맞다 / 틀리다
  // Boolean
  bool isTrue = true;
  bool isFalse = false;

  print(isTrue);
  print(isFalse);
}

void main() {
  // 글자 타입
  // String
  String name = '레드벨벳';
  String name2 = '코드팩토리';

  print(name + name2) //스트링끼리도 덧셈 가능 글자가 합쳐서 출력됨 덧셈만 됨!
  print('${name} ${name2}'); //스트링에 변수 값을 넣을 수 있다 ${} <- 괄호가 생략가능 &name
}

// var String 의 차이는? 
 var name3 = '블핑' //자동으로 스트링   //var는 오른쪽 값을 통해서 유추를 한다
 var number = 20;   //자동으로 integer

print(rentimeType) //실시간으로  값의 타입을 알려줌

// 다이나믹 타입
void main() {
dynamic name = '코드팩토리'; //다이나믹 타입은 어떤 타입이든 넣을 수 있다. 
dynamic number = 1;
//var과 dynamic의 차이가 뭔가?? var 타입은 한번 선언하면 다른 타입으로 변경이 불가능 dynamic은 선언해도 타입변경이 가능!!
}

// null,nullable
void main() {
  // nullable - null이 될 수 있다.
  //  non-nullable - null이 될 수 없다.
  //  null - 아무런 값도 있지 않다.

  String name = '토드팩토리';
  print(name);
  name = null // 오류 발생

  String? name2 = '블랙핑크';
  name2 = null; //오류가 발생하지 않는다 어떤 타입이더라도 ?를 붙이면 null값을 선언할 수 있다.

  print(name2!); //!를 붙이면 현재 이 값은 null이 아니다
}

//final,const
void main() {
 final String name = '코드팩토리'; //final로 변수값을 선언하면 값을 변경할 수 없다.'

 const String name2 = '블랙핑크'; //이친구도 값을 바꿀 수 없다. final과 const는 타입을 지정하지 않아도 된다.
// const와 final의 차이는? const는 빌드 타입 값을 알아야한다 final은 몰라도 됨!!
}

//
void main() {
  int number = 2;

  number ++; //1을 더하게 된다.
  number --; //1을 빼게 된다.
  number += 1; //1을 더해서 재저장!!
  number -= 1;
  number *= 2;
  number /= 2;
}

//null
void main() {
  double? number = 4.0;
  print(number);
  number = 2.0;
  print(number);
  number = null;
  print(number);

  number ??= 3.0; //?? number가 null일때 오른쪽 값(3.0)으로 바꿔라
}

//비교 연산자
void main() {

  int number1 = 1;
  int number2 = 2;
  print(number1 > number2); //false
  print(number1 < number2); //True
  print(number1 >= number2); //크거나 같은지
  print(number1 <= number2); //작거나 같은지
  print(number1 == number2); //number1과 number2값이 같은지
  print(number1 != number2); //number1과 number2값이 같지 않은지지
}

//타입 연산자
void main() {
  int number1 = 1;
  print(number1 is int); //True 타입이 맞는지
  print(number1 is String);  //false

  //타입이 아닌지는 is! 뒤에 느낌표를 붙이면 된다.
}

//논리 연산자
void main() {
  bool result = 12 > 10 && 1> 0; //둘다 true여야지 result가 true값이 나온다. True (and 연산자)
  bool result = 12 > 10 || 1 > 0; // 둘중 하나만 true이면 true값이 나온다. 둘다 false면 false(or 연산자)
}

//List
void main() {
  List<String> blackPink = ['제니', '지수', '로제', '리사'];
  List<int> number = [1,2,3,4,5,6];

  //index(순서)는 0부터 시작한다.
  print(blackPink[0]); // 제니
  print(blackPink[1]); // 지수
  print(blackPink[4]); // error

  print(blackPink.length); //List의 길이가 출력: 4
  blackPink.add('이정환'); // 리스트 마지막에 값을 넣을 수 있다.
  blackPink,remobe('이정환'); // 값을 지울 수 있다.
  print(blackPink.indexOf('로제')); // 주소값을 알 수 있다. 출력:2
}

//map
void main() {
  //map 값은 key,value 값을 같는다.
  Map<String, String> dictionary = { 'Harry Potter' : '해리포터, }; //왼쪽이 키값 오른쪽은 벨류 값 ,를 이용하여 값을 계속 저장 가능
  dictionary.addAll( { 'Spiderman': '이정환',}); // addAll을 이용해 값을 추가할 수 있다.
  print(dictionary['Spiderman']); //key 값을 이용해 value값을 출력할 수 있다.
  dictionary['Ron Weasley'] = '론 위즐리'; // 이렇게도 추가 가능, key값을 이용해 value값을 바꿀 수 도 있다.!!
  dictionary.remove('Harry Potter'); //remove를 이용해 삭제도 가능 key값을 이용함
  print(dictionary.keys); 키값을 다 가져올 수 있다.
  print(dictionary.value); value값을 다 가져올 수 있다.
}

//Set
void main() {
 // Set은 중복 되는값을 넣을 수 없다!!
  
  final Set<String> names = {
    'Code Factory',
    'Flutter',
    'Black Pink'
  };
  
  print(names);
  names.add('Jenny'); // 값을 추가
  names.remove('Jenny');// 값을 제거
  
  print(names.contains('Flutter')); //값이 존재하는지 확인 할 수 있다 출력: true 
}

//if
void main() {
 // if 문
  
  int number = 2;
  
  if(number % 2 == 0){  
    print('값이 짝수입니다');
     
  }
  else {
    print('값이 홀수 입니다.');
  }
}
//else if 를 이용해 조건식을 하나 더 만들 수 있다.!!!

// switch

void main() {
 // switch 문
  
  int number = 3;
  
  switch(number % 3) {
    case 0:
      print("나머지가 0입니다");
      break; //브레이크 문을 넣어줘야한다 그래야 다음 케이스를 보지 않음!!
      
    case 1:
      print("나머지가 1입니다.");
      break;
      
    default: //if 문에서 else와 같은 구문
      print("나머지가 2입니다.");
      break;
    
  }
}

//for
void main() {
 //for loop
  for(int i = 0; i < 10; i++) { //i가 0부터 10보다 작을때 까지 i값을 증가시켜라
    print(i);
  }
}
//for를 이용한 List
void main() {
 //for loop
  int total = 0;
  
  List<int> numbers = [1, 2, 3, 4, 5, 6];
  
  for(int i  = 0; i< numbers.length; i++) {
    
    total += numbers[i]; //i의 인덱스 값을 이용하여 리스트에 접근 가능
    
  }
  print(total); // 출력: 21
  
  total = 0;
  
  
  for(int number in numbers) { //numbers의 리스트에 있는 값을 하나씩 돌면서 number값에 받을 수 있다.
    print(number); //1부터 6까지 숫자들이 출력됨
    total += number; // 1부터 6까지 다 더한값이 출력됨.
  }
}

//While
void main() {
 // while loop
  
  int total = 0;
  
  while(total< 10){ //10보다 작을때가지 무한 loop가 돌지 않게 조심(항상 true)
    total += 1;
    
    if(total == 5) {
      break; // 5까지만 실행함 loop를 벗어남 5에서 for문에서도 마찬가지로 break문을 사용할 수 있다.!!
    }
  }
  
  print(total);
  
  do{ //먼저 +1을 하고 while문을 돈다 보통 do-while을 잘 안씀..
    total += 1;
  } while(total < 10);
  
  print(total);
}

//continue
void main() {
 // while loop
  
  for(int i = 0; i < 10; i++) {
    if(i == 5) {
      continue; // 현재 loop만 스킵! 출력은 5만 빼고 출력이 된다!!
      
    }
    print(i);
  }

//enume

enume Status { // enume을 사용하면 밑에 처럼 3가지 타입만 사용할 수 있게 강제할 수 있다. 따른 타입을 사용하면 에러가 뜸
approved,
pending,
rejected,
}

void main() {
Status status = Status.pending;

if(status == status.approved) {
  print('승인입니다');
}
else if (status == Status.pending) {
print('대기입니다.');
}
else {
print('거절입니다.');
}

//함수(parameter)

// positional parameter - 순서가 중요한 파라미터
void main() {
  
  addNumbers(10,20,30);

}
// 세개의 숫자 (x, y, z) 를 더하고 짝수인지 홀수인지 알려주는 함수
// parameter / argument - 매개변수
addNumbers(int x, int y, int z) { // 외부에서 받은 x y z 값을 이용해 밑에 로직을 실행할 수 있다.
  int sum = x + y + z;
  
  print('x : $x');
  print('y : $y');
  print('z : $z');


if (sum % 2 == 0) {
  print('짝수입니다.');
}
else {
  print('홀수입니다.');
 }
}

// optional parameter - 있어도 되고 없어도 되는 파라미터
void main() {
  
  addNumbers(10);
}
// 세개의 숫자 (x, y, z) 를 더하고 짝수인지 홀수인지 알려주는 함수
// parameter / argument - 매개변수
// 대괄호를 이용하여 함수를 넣지 않아도 된다. 대신 기본값을 정해줘야한다.
addNumbers(int x, [int y = 20 , int z = 30]) { 
  int sum = x + y + z;
  
  print('x : $x');
  print('y : $y');
  print('z : $z');


if (sum % 2 == 0) {
  print('짝수입니다.');
}
else {
  print('홀수입니다.');
 }
}

// named parameter - 이름이 있는 파라미터 (순서가 중요하지 않다.)
void main() {
  
  addNumbers(x: 10, y: 20, z: 30); // x,y,z 순서가 바뀌어도 상관이 없다.
}
// 세개의 숫자 (x, y, z) 를 더하고 짝수인지 홀수인지 알려주는 함수
// parameter / argument - 매개변수

addNumbers({
  required int x,
  required int y,
  required int z,
}) { 
  int sum = x + y + z;
  
  print('x : $x');
  print('y : $y');
  print('z : $z');


if (sum % 2 == 0) {
  print('짝수입니다.');
}
else {
  print('홀수입니다.');
 }
}


// void 
void main() {
  
int result = addNumbers(x: 10, y: 20, z: 30); // x,y,z 순서가 바뀌어도 상관이 없다.

  print('result: $result'); // 리턴값을 이용한 result 출력
}
// 세개의 숫자 (x, y, z) 를 더하고 짝수인지 홀수인지 알려주는 함수
// parameter / argument - 매개변수

int addNumbers({
  required int x,
  required int y,
  required int z,
}) { 
  int sum = x + y + z;
  
  print('x : $x');
  print('y : $y');
  print('z : $z');


if (sum % 2 == 0) {
  print('짝수입니다.');
}
else {
  print('홀수입니다.');
 }
  
  return sum; // return을 이용하여 값을 반환할 수 있다.
}


// arrow function - 화살표 함수를 이용해서 값을 리턴할 수 있다
void main() {
  
int result = addNumbers(x: 10, y: 20, z: 30); // x,y,z 순서가 바뀌어도 상관이 없다.

  print('result: $result'); // 리턴값을 이용한 result 출력
}
// 세개의 숫자 (x, y, z) 를 더하고 짝수인지 홀수인지 알려주는 함수
// parameter / argument - 매개변수

int addNumbers({
  required int x,
  required int y,
  required int z,
}) => x + y + z;
 
//typedef 같은 타입을 같는 메소드를 호출

void main() {
  Operation operation = add;
  
  int result = operation(10, 20, 30);
  print(result); //add함수가 실행된다. 출력: 60
  
  operation = subtract;
  int result2 = operation(10, 20, 30);
  print (result2); // subtract함수가 실행된다.
  
  
  int result3 = calculate( 30, 40, 50, add);
  print (result3); // 실질적으로 이렇게 많이 쓰임 operation에 대한 x,y,z 리턴값 실행
  
  
}

typedef Operation = int Function(int x, int y, int z); //타입이 일치해야한다

// 더하기
int add(int x, int y, int z) => x+y+z;

// 빼기
int subtract(int x, int y, int z) => x-y-z;

int calculate(int x, int y, int z, Operation operation) {
  return operation(x, y, z);
}





  








 
      
                                    
                                    
                                    
                        
  
  
  
  

  




