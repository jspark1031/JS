1. JavaScript의 자료형
JavaScript의 원시 타입(Primitive)은 변수에 값이 직접 담기며, Java와 달리 정수(int, long)와 실수(double, float)를 구분하지 않고 number 하나로 다룹니다.

number: 정수, 실수, 특수 숫자(NaN, Infinity)를 포함합니다.

string: 작은따옴표('...'), 큰따옴표("..."), 백틱(`...`)으로 감싼 문자열입니다.

boolean: true 또는 false 논리값입니다.

null: "값이 비어 있음"을 의도적으로 나타낼 때 사용합니다.

undefined: 변수를 선언만 하고 값을 할당하지 않았을 때 자동으로 들어가는 "값이 아직 정해지지 않음" 상태입니다.

JavaScript
let score = 95;          // number (정수)
let ratio = 0.85;        // number (실수)
let grade = "A";         // string (Java의 char 타입이 별도로 없음)
let isPassed = true;     // boolean
let selectedItem = null; // null (의도적 빈 값)
let notAssigned;         // undefined (할당 전 기본값)

console.log(score, ratio, grade, isPassed, selectedItem, notAssigned);

=================================================================

2. JavaScript의 변수 선언
Java처럼 int x = 10;처럼 타입을 앞에 쓰지 않고, 재할당 가능 여부에 따라 let과 const를 선택합니다. (과거의 var는 스코프 문제로 현대 코드에서는 피하는 추세입니다.)

let: 재할당 가능한 변수입니다. Java의 일반 변수와 비슷합니다.

const: 재할당이 불가능한 상수입니다. 선언과 동시에 초기화해야 하며, Java의 final과 유사합니다. 단, const로 선언한 객체나 배열의 내부 속성/요소 변경은 가능합니다.

JavaScript
let count = 1;
count = 2; // 가능: let은 재할당 허용

const MAX_USERS = 100;
// MAX_USERS = 200; // 오류(TypeError): const는 재할당 불가

const user = { name: "민수" };
user.name = "지훈"; // 가능: 참조(주소)가 바뀌는 것이 아니라 내부 속성 변경
console.log(count, MAX_USERS, user);

=================================================================

3. JavaScript의 연산 방법
산술 연산자(+, -, *, /, %)는 Java와 거의 같지만, 정수 나눗셈 규칙이 다릅니다. Java에서는 5 / 2가 2가 되지만, JavaScript에서는 2.5가 나옵니다.

+ 더하기 / - 빼기 / * 곱하기 / / 나누기 / % 나머지 연산: 표준 산술 연산자입니다.

Math 내장 객체: 수학 계산을 돕는 내장 객체로, Java의 Math 클래스와 비슷하게 정적 메서드 형태로 씁니다(Math.max, Math.floor, Math.round, Math.pow, Math.random 등).

JavaScript
console.log(10 + 3); // 13
console.log(10 - 3); // 7
console.log(10 * 3); // 30
console.log(10 / 3); // 3.3333333333333335 (Java와 달리 실수 나눗셈)
console.log(10 % 3); // 1 (나머지)

// Math 내장 객체 활용
console.log(Math.floor(3.7)); // 3 (내림)
console.log(Math.ceil(3.1));  // 4 (올림)
console.log(Math.round(3.5)); // 4 (반올림)
console.log(Math.max(10, 25, 7)); // 25
console.log(Math.random());     // 0 이상 1 미만 난수

=================================================================

4. JavaScript의 비교 연산
Java에서는 참조 타입의 동등성을 equals()로 비교하지만, JavaScript에서는 ==와 === 연산자를 사용합니다. 실무에서는 암묵적 타입 변환으로 인한 혼란을 막기 위해 === 사용을 권장합니다.

<, >, <=, >=: 값의 대소 비교입니다. 문자열끼리 비교하면 사전식(유니코드) 순서로 비교합니다.

== (동등 연산자): 타입이 다르면 자동으로 타입을 맞춘 뒤 값을 비교합니다.

=== (일치 연산자): 타입 변환 없이 타입과 값이 모두 같을 때만 true를 반환합니다.

typeof: 값이나 변수의 자료형을 문자열로 반환하는 연산자입니다. (단, typeof null이 "object"로 나오는 것은 JavaScript의 오래된 역사적 quirk입니다.)

JavaScript
console.log(10 > 5, 10 <= 10); // true, true
console.log("apple" < "banana"); // true

// == vs === 차이
console.log(5 == "5");  // true  ("5"를 숫자 5로 변환해 비교)
console.log(5 === "5"); // false (number와 string으로 타입이 다름)
console.log(null == undefined);  // true
console.log(null === undefined); // false

// typeof 확인
console.log(typeof 42);        // "number"
console.log(typeof "hello");   // "string"
console.log(typeof true);      // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof null);      // "object" (주의해야 할 특징)

=================================================================

5. JavaScript의 논리 연산
Java와 동일하게 &&, ||, !를 사용하며 단락 평가(Short-circuit evaluation)가 동작합니다. JavaScript에서는 &&와 ||가 불리언뿐만 아니라 피연산자 값 자체를 반환하기도 합니다.

&& (AND): 앞 조건이 거짓(falsy)이면 뒤를 평가하지 않고 거짓/앞 값을 반환하며, 모두 참이면 뒤 값을 반환합니다.

|| (OR): 앞 조건이 참(truthy)이면 뒤를 평가하지 않고 앞 값을 반환하며, 앞이 거짓이면 뒤 값을 반환합니다. (기본값 설정에 자주 씁니다.)

! (NOT): 불리언 값을 반전시킵니다.

JavaScript
let age = 22;
let hasId = true;

console.log(age >= 20 && hasId); // true
console.log(age < 18 || hasId);  // true
console.log(!hasId);             // false

// 값 자체를 반환하는 활용 예시 (기본값 폴백)
let nickname = "";
let displayName = nickname || "익명사용자";
console.log(displayName); // "익명사용자"

=================================================================

6. JavaScript의 문자열 연산
Java에서 +로 문자열을 이어 붙이거나 String.format()을 쓰듯, JavaScript는 +와 템플릿 리터럴을 사용합니다.

+ 이어붙이기: 문자열과 다른 값을 +로 연결합니다.

템플릿 리터럴: 백틱(`) 안에서 ${표현식} 문법으로 변수나 계산식을 바로 끼워 넣을 수 있습니다. 줄바꿈도 그대로 유지됩니다.

number + string 연산 시 Python과의 차이점:

JavaScript: 숫자가 문자열로 자동 변환되어 문자열 연결이 됩니다(10 + "5" → "105"). Java의 "값: " + 10 동작과 비슷합니다.

Python: 10 + "5"처럼 숫자와 문자열을 +로 직접 더하면 TypeError가 발생합니다(명시적으로 str(10)으로 변환해야 함).

JavaScript
let name = "서연";
let points = 120;

// + 이어붙이기
let msg1 = "안녕하세요, " + name + "님!";

// 템플릿 리터럴 (백틱 + ${...})
let msg2 = `안녕하세요, ${name}님! 현재 포인트는 ${points * 2}점입니다.`;

// number + string 연산
console.log(10 + "5"); // "105" (JavaScript: 문자열로 이어붙임, Python에서는 TypeError)
console.log("10" - 3); // 7     (-, *, / 같은 산술 연산자는 문자열을 숫자로 변환 시도)
console.log(msg1);
console.log(msg2);

=================================================================

7. JavaScript의 조건문
Java와 문법 구조가 매우 비슷합니다. 다만 Python의 elif가 아니라 else if를 사용합니다.

JavaScript
let score = 84;

if (score >= 90) {
  console.log("학점: A");
} else if (score >= 80) {
  console.log("학점: B");
} else {
  console.log("학점: C 이하");
}

=================================================================

8. JavaScript의 반복문
Java의 for (int i = 0; i < n; i++)와 while (조건) 형태를 그대로 사용할 수 있습니다. 배열이나 객체를 순회할 때는 for...of, for...in도 자주 쓰입니다.

JavaScript
// for 문
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue; // 3은 건너뜀
  console.log("for i =", i);
}

// while 문
let countdown = 3;
while (countdown > 0) {
  console.log("남은 시간:", countdown);
  countdown--;
}

=================================================================

9. JavaScript의 배열
Java의 ArrayList처럼 길이가 동적으로 변하고, 한 배열 안에 서로 다른 타입의 값도 함께 담을 수 있습니다. 대괄호 [ ... ]로 만듭니다.

array 사용법: 인덱스로 접근(arr[0]), .length로 길이 확인, .push() / .pop() 등으로 요소를 추가·제거합니다.

array의 활용: .map(), .filter(), .forEach() 같은 고차 메서드로 데이터를 가공하거나 필터링하는 패턴이 매우 흔합니다.

JavaScript
// 배열 선언 및 기본 조작
let fruits = ["사과", "바나나"];
fruits.push("포도");      // 끝에 추가 -> ["사과", "바나나", "포도"]
console.log(fruits[0]);     // "사과"
console.log(fruits.length); // 3

let removed = fruits.pop(); // 끝 요소 제거 후 반환 -> "포도"
console.log(removed, fruits);

// 배열 활용: map, filter
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map((n) => n * 2);         // [2, 4, 6, 8, 10]
let evenNumbers = numbers.filter((n) => n % 2 === 0); // [2, 4]
console.log(doubled, evenNumbers);

=================================================================

10. JavaScript의 객체 자료형
JavaScript의 object는 키(key)-값(value) 쌍의 집합으로, Java의 Map이나 클래스 인스턴스 속성과 비슷한 역할을 합니다. 중괄호 { ... }로 선언합니다.

object 선언 방법: { 키: 값, ... } 형태로 작성합니다.

속성 읽기: 점 표기법(obj.key) 또는 대괄호 표기법(obj["key"], 동적 키 이름이나 공백·특수문자가 있는 키에 유용)을 씁니다.

속성 추가하기 / 수정하기: 존재하지 않는 키에 값을 대입하면 추가되고, 기존 키에 대입하면 수정됩니다.

속성 제거하기: delete obj.key로 속성을 삭제합니다.

속성 존재 확인 (in): "key" in obj 형태로 해당 키가 객체(또는 프로토타입 체인)에 존재하는지 boolean으로 확인합니다.

JavaScript
// 1. object 선언
let member = {
  id: 101,
  name: "도윤",
  role: "member"
};

// 2. 속성 읽기
console.log(member.name);    // "도윤"
console.log(member["role"]); // "member"

// 3. 속성 추가하기 & 수정하기
member.email = "doyun@example.com"; // 추가
member.role = "admin";              // 수정
console.log(member);

// 4. 속성 제거하기
delete member.id;
console.log(member); // { name: "도윤", role: "admin", email: "doyun@example.com" }

// 5. 속성이 객체에 존재하는지 확인하기 (in)
console.log("email" in member); // true
console.log("id" in member);    // false