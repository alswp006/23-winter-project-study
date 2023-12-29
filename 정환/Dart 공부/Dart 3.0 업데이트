## Record

List를 규격화 하여 표현할 수 있는 기능 타입과 타입의 순서를 보장받을 수 있음!

```dart
void main() {
  
  final result1 = nameAndAge( {
    'name': '민지',
    'age' : 20,
  });
  
  print(result1);
  print(result1.$1);
  print(result1.$2);
  
  final result = getMinji();
  print(result);
  
  final result2 = getNewJeansWithType();
  
  for(final item in result2) {
    print(item.$1);
    print(item.$2);
    
    final result3 = getNewJeansWithType2();
    print(item.$1);
    print(item.$2);
  }

}

//record
(String, int) nameAndAge(Map<String, dynamic> json) {
  return (json['name'] as String, json['age'] as int);
  
}

(String name, String group, int age) getMinji() {
  return ('민지', '뉴진스', 19);
}

// Record를 사용하지 않을때 type보장이 안되서 dynamic를 사용해야함
List<Map<String, dynamic>> getNewJeans() {
  return [
    {
  'name': '민지',
  'age' : 20,
},
    {
      'name': '혜린',
  'age' : 18,
    }
    ];
}

// Record

List<(String, int)> getNewJeansWithType() {
  return [
    (
    '민지',
    20,
    ),
    
    (
    '혜린',
    18,),
    ];
}

=
List<(String name, int age)> getNewJeansWithType2(){
   return [
    (
    '민지',
    20,
    ),
    
    (
    '혜린',
    18,),
    ];
}
```

## Restructure

**변수 쉽게 저장해서 print 할 수 있음**

```dart
void main() {
  final (name, age) = ('민지',20);
  
  print(name);
  print(age);
  
  
  //리스트에서
  final newJeans = ['민지', '해린'];
  final [String a, String b] = newJeans;
  
  print(a);
  print(b);

final numbers = [1,2,3,4,5,6,7,8];
  
  final [x, _, y, ...rest2, z, _] = numbers;
  
  print(x);
  print(y);
  print(z);
  print(rest2);
}
//map에서

final minJiMap = { 'name':'민지', 'age':19};
final {'name' : name3, 'age' : age3} = minJiMap;
print(name3);
print(age3);
```

## Validation

업데이트된 switch구문

```dart
void main() {
  
  switcher('aaa');
  switcher(['1','2']);
  switcher([1,2,3]);
  switcher([6, 9]);

}

void switcher(dynamic anything) {
  
  switch(anything) {
    case 'aaa':
      print('match:aaa');
    case ['1','2']:
      print('match: [1,2]');
    case [_,_,_]:
      print('match: [_,_,_]');
    case [int a, int b]:
      print('match: [int $a, int $b]');
    default:
      print('no match');
  }
}

String switcher2(dynamic val, bool condition) => switch (val){
    5 => 'match:5',// 스위치에서도 반환 가능
};
```

## final Class

extends, implement, mixin으로 사용이 불가능 하다

```dart
void main() {
  
}

// final로 클래스를 선언하면
// extends, implement, 또는 mixin으로 사용이 불가능하다.

final class Person {
  final String name;
  final int age;
  
  Person( {
    required this.name,
    required this.age,
  });
  
}
```

## base Class

base로 선언하면 extend는 가능하지만 implement는 불가능 extend와 implement구분이 가능
base, sealed, final로 선언된 클래스만 extend가 가능하다.

```dart
void main() {
  
 

}

// base로 선언하면 extend는 가능하지만 implement는 불가능
// base, sealed, final로 선언된 클래스만 extend가 가능하다.
base class Person {
  final String name;
  final int age;
  
  Person( {
    required this.name,
    required this.age,
  });
  
}
```

## interface class

interface로 선언하면 implement만 가능하다

```dart
void main() {
  

}
// interface로 선언하면 implement만 가능하다
interface class Person {
  final String name;
  final int age;
  
  Person( {
    required this.name,
    required this.age,
  });
  
}
```
