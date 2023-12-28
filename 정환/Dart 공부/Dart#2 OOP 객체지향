## Class 의 정의

클래스에는 변수와 함수가 있다. (ex 설계서를 만들어 내는것_

**instance**: 인스턴스를 생성해서 클래스의 정의된 기능들을 무한하게 생성가능 하다 (ex 클래스를 이용해 결과물을 만들어 내는 것)

**class 선언**

```dart
void main() {
  
}

// 클래스 선언
// name (이름)
// member (멤버들) - 변수
// sayHello (인사) - 함수
// introduce (멤버소개) - 함수

class Idol {
  String name = '블랙핑크';
  List<String> members = ['지수','제니','리사','로제'];
  
  
  void sayHello() {
    print("안녕하세요 블랙핑크입니다.");
  }
  
  void introduce() {
    print('저희 멤버는 지수, 제니, 리사, 로제가 있습니다.')
  }
}
```

**instance 선언**

```dart
void main() {
  Idol blackPink = Idol(
  '블랙핑크',
['지수','제니','리사','로제'],
);

 Idol blackPink2 = Idol(
  '블랙핑크',
['지수','제니','리사','로제'],
);
// 블랙핑크와 블랙핑크2의 변수들의 내용은 같으나 컴퓨터 프로그램에서 둘 값은 다른값이다.
// const로 선언하고 모든 멤버들을 같은 값으로 저장하면 변수값이 같은값이 되게 할 수 있다!!

print(blackPink.name);
}

```

**constructor(생성자): 클래스에서도 파라미터를 받아서 생성할 수 있다.**

```dart
void main() {
  Idol blackPink = const Idol(
  '블랙핑크',
['지수','제니','리사','로제'],
);

print(blackPink.name);
print(blackPink.members);
blackPink.sayHello();
blackPink.introduce();
}
// 클래스 선언
// name (이름)
// member (멤버들) - 변수
// sayHello (인사) - 함수
// introduce (멤버소개) - 함수

class Idol {
  final String name;
  final List<String> members;
  
  const Idol(this.name, this.members);
  
  
  
  void sayHello() {
    print("안녕하세요 ${this.name}입니다.");
  }
  
  void introduce() {
    print('저희 멤버는 ${this.members}가 있습니다.');
  }
}
```

**immutable 프로그래밍**:  프로그래밍 할때 한 변수를 계속 재사용하는 것이 비효율적일 가능성이 높다. 따라서 특수한 경우가 아니라면, class 내부의 변수들도 final을 통해 선언해 주는 것이 효율적! 변수값을 바꾸지 않게 하도록

클래스 변수로 final, const로 선언

```dart
void main() {
  Idol blackPink = Idol(
  '블랙핑크',
['지수','제니','리사','로제'],
);

print(blackPink.name);
print(blackPink.members);
blackPink.sayHello();
blackPink.introduce();
}
// 클래스 선언
// name (이름)
// member (멤버들) - 변수
// sayHello (인사) - 함수
// introduce (멤버소개) - 함수

class Idol {
  final String name; //final 선언 
  final List<String> members;
  
  const Idol(this.name, this.members);
  
  
  
  void sayHello() {
    print("안녕하세요 ${this.name}입니다.");
  }
  
  void introduce() {
    print('저희 멤버는 ${this.members}가 있습니다.');
  }
}
```

**Class의 getter / setter**

**getter은 데이터를 가져올때 / setter은 데이터를 설정할때**

```dart
String get firstMember { 
  return this.members[0];
  }
  
  // setter 무조건 한개의 파라미터만 들어갈 수 있다.
  set firstMember(String name) {
    this.members[1] = name;  // 값을 변경할 수 있다
  }
}
```

**private: 외부에서 파일들을 불러와도 사용할 수 없다 클래스명이나 변수명 앞에 _(underscore) 를 붙이면 된다.!**

```dart
class _MyAppState extends State<MyApp> {
  var _num = 0;
  void _addNum() {
    num++;
  }
 
}
```

**inheritance(상속): 상속을 받으면 부모 클래스의 모든 속성을 자식클래스가 부여받는다. 모든 속성들을 다 사용할 수 있다.**

```dart
void main() {
  
  print ('----------idol-----------');
  Idol apink = Idol(name: '에이핑크', membersCount:5);
  
  apink.sayName();
  apink.sayMembersCount();
  //자식 클래스에서 부모클래스에 속성을 넘겨줄 수 는 없다.!!
  
  print ('----------Boy Group-----------');
  BoyGroup bts = BoyGroup('BTS',7);
  bts.sayMembersCount();
  bts.sayName(); //idol안에있는 메소드를 전부 상속 받아서 사용할 수 있다.
  bts.sayMale(); //Girl Group에 있는 속성은 사용할 수 없다.!
  
  print ('----------Girl Group-----------');
  GirlGroup redVelvet = GirlGroup('Red Velvet', 5);
  
  redVelvet.sayMembersCount();
  redVelvet.sayName();
  redVelvet.sayFemale();
 
}

class Idol {
  
  String name;
  int membersCount;
  
  Idol( { // named parameter 이름이 있는 파라미터
    required this.name,
    required this.membersCount,
  });
  
  void sayName() {
    print('저는 ${this.name}입니다.');
  }
  
  void sayMembersCount() {
    print('${this.name}은 ${this.membersCount}명의 멤버가 있습니다.');
  }
  
}
//inheritance
class BoyGroup extends Idol {
  BoyGroup(
  String name,
  int membersCount,
  ): super(  //부모클래스를 지칭하는건 super()
  name: name,
  membersCount: membersCount,
  );
  
  void sayMale() {
    print("저는 남자 아이돌입니다.");
  }
  
}

class GirlGroup extends Idol {
  GirlGroup(
  String name,
  int membersCount,
  ): super(
  name: name,
  membersCount: membersCount,
  );
  
  void sayFemale() {
    print("저는 여자 아이돌입니다.");
  }
}
```

**method: function (class 내부에 있는 함수)**

**override - 덮어쓰다 (우선시하다)**

```dart
void main() {
  
  TimesTwo tt = TimesTwo(2);
  
  print(tt.calculate());
  
  TimesFour tf = TimesFour(2);
  print(tf.calculate());
 
}

class TimesTwo {
  final int number;
  
  TimesTwo( //생성자 class에 파라미터 값을 받아서 사용하기 위함
    this.number,
    );
    
    // method
    int calculate() {
      return number *2;
    }
  }

class TimesFour extends TimesTwo {
  TimesFour( 
  int number,
  ) : super(number);
  
  
  @override
  int calculate(){ // 부모클래스에 있는 calculator 함수를 현재 클래스에서
 // 덮어쓸 수 있다. override
    return super.calculate() *2; 
    //부모 클래스의 메소드를 그대로 가져 올 수 있다.! 추가적인 계산이나 로직을 넣을 수 있음
  }
}
```

**static - class나 인스턴스에 변수를 귀속 시킬 수 있다.**

```dart
void main() {
  Employee seulgi = Employee('슬기');
  Employee chorong = Employee('초롱');
  
  seulgi.name = '코드팩토리'; //이렇게 값을 바꾸어도 인스턴스마다 값이 각각 다르다
  seulgi.printNameAndBuilding();
  chorong.printNameAndBuilding();
  
  Employee.building = '오투타워';
  seulgi.printNameAndBuilding();
  chorong.printNameAndBuilding(); //클래스에 귀속되는 값은 둘다 모두 같이 바뀐다.
  
  Employee.printBuilding(); // static 메소드
}

class Employee {
  //static은 instance에 귀속되지 않고 class에 귀속된다.!!
  // 알바생이 일하고 있는 건물
  static String? building; // 자 여기서 물음표는 null값이 들어가도 되는 String
  // 알바생 이름
  String name;
  
  Employee(
    this.name,
  );
  
  void printNameAndBuilding() {
    print('제 이름은 $name입니다. $building 건물에서 근무하고 있습니다.');
  }
  
  static void printBuilding() {
    print('저는 $building 건물에서 근무중입니다.');
  }
  
}
```

**Interface: 어떤 특수하게 설계한 구조를 강제한다. 상속과 살짝 다르다**

```dart
void main() {
  BoyGroup bts = BoyGroup('BTS');
  GirlGroup redVelvet = GirlGroup('레드벨벳');
  IdolInterface test = IdolInterface('블랙핑크'); // 인스턴스화 하면 안된다 인터페이스는
  
  bts.sayName();
  redVelvet.sayName();
  
  
}

//interface 인스턴스로 사용하면 안됨!
abstract class IdolInterface { //abstract로 만들면 인터페이스를 인스턴스화 하는걸 막을 수 있다.
  String name;
  
  IdolInterface(this.name);
  
  void sayName(); //abstract로 만들면 함수의 바디{}를 지워도 된다.
}

class BoyGroup implements IdolInterface {
  
  String name;
  
  BoyGroup(this.name);
  
  void sayName(){
    print('제 이름은 $name입니다.');
  } //강제로 위 인터페이스와 맞춰야 함 이게 특징임!
  
}

class GirlGroup implements IdolInterface {
  
  String name;
  
  GirlGroup(this.name);
  
  void sayName(){
    print('제 이름은 $name입니다.');
  
  }
}
```

**generic: 타입을 외부에서 받을때 사용**

```dart
void main() {
   Lecture<String> lecture1 = Lecture('123', 'lecture1');
   lecture1.printIdType();
   
 }

// generic - 타입을 외부에서 받을때 사용

class Lecture<T> { // 클래스 명 옆에 <아무 문자나> 이용, 타입을 여러개 받을 수 있다
  final T id; //외부에서 타입을 마음대로 지정
  final String name;
  
  Lecture(this.id, this.name);
  
  void printIdType() {
    print(id.runtimeType); // id 타입을 알려준다
  }
  
}
```

**Object Class: 모든 클래스의 최상위 클래스**
