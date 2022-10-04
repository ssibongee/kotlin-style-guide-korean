# Kotlin Style Guide 한국어 번역글

[Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html) 

# Coding conventions
일반적으로 알려진 따르기 쉬운 코딩 컨벤션은 모든 프로그래밍 언어에 필수적입니다. 여기에서는 Kotlin을 사용하는 프로젝트의 코드 스타일 및 코드 구성에 대한 가이드라인을 제공합니다.

# Configure Style in IDE
Kotlin을 위해 가장 많이 사용되는 두 가지 IDE인 IntelliJ IDEA와 Android Studio는 코드 스타일링을 위한 강력한 지원을 제공합니다. 주어진 코드 스타일에 따라서 코드를 자동으로 포멧하도록 구성할 수 있습니다.

## Apply the style guide
1. **Settings/Preferences | Editor | Code Style | Kotlin** 으로 이동합니다.
2. **Set from...** 을 클릭합니다.
3. **Kotlin style guide** 를 선택합니다.

# Source Code

## Source File Names

파일의 이름은 파일의 코드가 수행하는 작업을 설명해야 합니다. 따라서 파일 이름에 `Util` 과 같은 의미없는 단어를 사용하지 않아야 합니다.


## Source File Organization
동일한 Kotlin 소스 파일에 여러 선언(클래스 및 최상위 함수 또는 속성)을 배치하는 것은 이러한 선언이 의미적으로 서로 밀접하게 관련되어있고 파일의 크기가 합리적으로 유지되는 범위 내에서(수백줄을 초과하지 않는 정도) 권장됩니다.

특히, 클래스의 모든 클라이언트와 관련된 클래스에 대한 확장 함수를 정의할 때 클래스와 동일한 파일에 정의합니다. 특정 클라이언트에서만 의미가 있는 확장 함수를 정의할 때 해당 클라이언트 코드에 위치하십시오. 일부 클래스의 모든 확장들을 가지고 있기위해 파일을 생성하지 마십시오.

## Class Layout
클래스의 내용들은 다음의 순서를 따라야합니다.
1. 속성 선언 및 초기화 블록
2. 보조 생성자
3. 메서드 선언
4. 동반(Companion) 객체

메서드의 선언을 알파벳 순서 또는 가시성을 기준으로 정렬하지 마십시오, 또한 일반 메서드와 확장 메서드를 분리하지 마십시오. 
대신, 관련된 내용을 함께 모아서 클래스를 위에서 아래로 읽는 누군가가 무슨 일이 일어나고있는지 이해할 수 있도록 작성하세요. 순서를 선택하고(높은 수준의 항목을 먼저 선택하거나 그 반대로) 따르세요.

중첩된 클래스는 해당 클래스를 사용하는 코드 옆에 배치합니다. 클래스가 외부에서 사용되도록 의도되고 클래스 내부에서 참조되지 않는 경우 클래스는 마지막에 동반 객체 뒤에 배치합니다.

## Interface Implementation Layout
인터페이스를 구현할 때 구현하는 멤버들을 인터페이스의 멤버들과 같은 순서로 유지하세요. (필요한 경우 구현에 사용되는 `private` 메서드가 산재되어있을 수 있습니다.)

## Overload Layout
클래스에서 오버로드한 항목들을 같이 배치하세요.

# Naming Rule
Kotlin의 패키지 및 클래스 명명 규칙은 매우 간단합니다.

- 패키지 이름은 항상 소문자이며 `_`를 사용하지 않습니다. (`org.example.project`) 여러 단어로 이루어진 이름을 사용하는 것은 일반적으로 권장되지 않지만 여러 단어를 사용해야하는 경우에는 이들을 함께 연결하거나 카멜 케이스를 사용할 수 있습니다.(`org.example.myProject`)
- 클래스 및 오브젝트 클래스의 이름은 대문자로 시작하고 카멜 케이스를 사용합니다.

```kotlin
open class DeclarationProcessor { /* ... */ }

object EmptyDeclarationProcessor : DeclarationProcessor() { /* ... */ }
```

## Function Names
함수, 속성 및 지역 변수의 이름은 소문자로 시작하고 `_` 없이 카멜 케이스 대소문자를 사용합니다.
```kotlin
fun processDeclarations() { /* ... */ }
var declarationCount = 1
```

Exception: 클래스의 인스턴스를 만드는데 사용되는 팩토리 메서드는 반환되는 추상 타입과 동일한 이름을 가질 수 있습니다.
```kotlin 
interface Foo { /*...*/ }

class FooImpl : Foo { /*...*/ }

fun Foo(): Foo { return FooImpl() }
```

## Names for Test Methods
테스트에서(**테스트에서만**) 백틱(`` ` ``)으로 묶인 공백이 있는 메서드 이름을 사용할 수 있습니다. 이러한 메서드 이름은 현재 Android 런타임에서 지원되지 않습니다. 테스트 코드에서 메서드 이름에서의 `_` 사용도 허용됩니다.
```kotlin
class MyTestCase {
     @Test fun `ensure everything works`() { /*...*/ }

     @Test fun ensureEverythingWorks_onAndroid() { /*...*/ }
}
```

## Property Names
상수 이름(`const`로 표시된 속성 또는 완전히 변경 불가능한 데이터를 보유하고있는 커스텀 `get` 함수가 없는 최상위 또는 `object`의 `val`속성)은 `_`로 구분된 대문자로 이루어진 이름을 사용해야 합니다. ([screaming snake case](https://papago.naver.net/apis/site/proxy?url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FSnake_case))
```kotlin
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserName"
```
동작 또는 변경 가능한 데이터가 있는 객체를 보유하는 최상위 또는 `object`의 속성 이름은 카멜 케이스 대소문자 이름을 사용해야 합니다.
```kotlin
val mutableCollection: MutableSet<String> = HashSet()
```
싱글톤 객체에 대한 참조를 보유하는 속성의 이름은 `object` 선언과 동일한 명명 스타일을 사용할 수 있습니다.
```kotlin
val PersonComparator: Comparator<Person> = /*...*/
```
열거형 상수의 경우 사용법에 따라서 대문자와 `_`로 구분된 이름(screaming snake case) (`enum class Color { RED, GREEN }`) 또는 대문자 카멜 케이스 이름을 사용할 수 있습니다.

## Naming for Backing Properties
클래스에는 개념적으로 동일한 두 개의 속성이 있지만 하나는 `public` API의 일부이고 다른 하나는 구현 세부 정보인 경우 `private` 속성 이름의 접두사로 `_`를 사용합니다.
```kotlin
class C {
     private val _elementList = mutableListOf<Element>()
     
     val elementList: List<Element>
          get() = _elementList
}
```

## Choose Good Names
클래스 이름은 일반적으로 명사 또는 클래스가 무엇인지를 설명하는 명사구 입니다: `List`, `PersonReader`.

메서드 이름은 일반적으로 메서드가 하는 일을 나타내는 동사 또는 동사구 입니다: `close`, `readPersons`. 이름은 또한 메서드가 객체를 변경하거나 새로운 객체를 반환하는지 여부를 암시해야 합니다. 예를들어 `sort`는 컬렉션을 제자리에서 정렬하고, `sorted`는 컬렉션의 정렬된 복사본을 반환합니다.

이름은 엔티티의 목적이 무엇인지 명확해야 하기 때문에 이름에 의미없는 단어(`Manager`, `Wrapper`)를 사용하지 않는 것이 가장 좋습니다.

선언된 이름의 일부로 줄임말(acronym)를 사용할 때 두 글자로 구성된 경우(`IOStream`) 대문자로 표시합니다. 길이가 긴 경 첫글자만 대문자로 표시합니다. (`XmlFormatter`, `HttpInputStream`)

# Formatting

## Indentation
들여쓰기에는 4개의 공백을 사용합니다. 탭을 사용하지 마십시오.

중괄호의 경우 여는 중괄호 구문이 시작하는 줄 끝에 위치하고 닫는 중괄호를 여는 구문과 수평으로 정렬된 별도의 줄에 위치시킵니다.
```kotlin
if (elements != null) {
     for (element in elements) {
          // ...
     }
}
```
> Kotlin에서 세미콜론은 선택사항이므로 줄 바꿈이 중요합니다. 언어 디자인은 Java 스타일 중괄호를 사용하며 다른 형식 지정 스타일을 사용하려고하면 의도치 않은 동작이 발생할 수 있습니다.

## Horizontal Whitespace
- 이항 연산자 주변에 공백을 넣습니다.(`a + b`)
  Exception: 범위 연산자 주변에 공백을 두지 마십시오. (`0..i`)
- 단항 연산자 주변에 공백을 두지 마십시오. (`a++`)
- 제어 흐름 키워드(`if`, `when`, `for` 및 `while`)와 해당 여는 괄호 사이에 공백을 넣습니다.
- 기본 생성자 선언, 메서드 선언 또는 메서드 호출에서 여는 괄호 앞에 공백을 두지 마십시오.
```kotlin
class A(val x: Int)

fun foo(x: Int) { ... }

fun bar() {
    foo(1)
}
```
- `(`, `[` 또는 `]`, `)` 앞에 공백을 두지 마십시오.
- `.` 또는 `?.` 주변에 공백을 두지 마십시오. `foo.bar().filter { it > 2 }.joinToString()` , `foo?.bar()`
- `//` 뒤에 공백을 넣으세요. `// This is a comment`
- 타입 파라미터를 지정하는데 사용되는 꺽쇠 괄호 주위에 공백을 두지 마십시오. `class Map<K, V> { ... }`
- `::` 주위에 공백을 두지 마십시오. `Foo::class`, `String::length`
- `nullable` 타입을 표시하는데 사용되는 `?` 전에 공백을 두지 마십시오. `String?`

일반적으로 어떠한 종류의 수평 정렬을 피하세요. 식별자의 이름을 길이가 다른 이름으로 변경해도 선언 형식 또는 사용 방법에 영향을 주지 않아야 합니다.

## Colon
다음의 경우 `:` 앞에 공백을 넣으세요.
- 타입과 슈퍼 타입을 구분하기 위해 사용되는 경우
- 슈퍼 클래스 생성자나 같은 클래스의 다른 생성자에게 위임하는 경우
- `object` 키워드 뒤에 
`:` 이 타입과 선언을 구분할 때는 앞에 공백을 두지 마세요.

항상 `:` 뒤에 공백을 넣으세요.
```kotlin
abstract class Foo<out T : Any> : IFoo {
    abstract fun foo(a: Int): T
}

class FooImpl : Foo() {
    constructor(x: String) : this(x) { /*...*/ }

    val x = object : IFoo { /*...*/ }
}
```

## Class Headers
적은 수의 기본 생성자 매개변수들이 있는 클래스는 한 줄에 작성할 수 있습니다.
```kotlin
class Person(id: Int, name: String)
```

헤더가 긴 클래스는 각 기본 생성자 매개변수가 들여쓰기가 있는 별도의 라인에 위치하도록 형식을 지정해야 합니다. 또한 닫는 괄호는 새로운 줄에 위치해야합니다. 상속을 사용하는 경우 슈퍼 클래스 생성자 호출 또는 구현된 인터페이스 목록이 괄호와 같은 줄에 있어야 합니다.
```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name) { /*...*/ }
```

다중 인터페이스의 경우 슈퍼 클래스 생성자 호출을 먼저 배치하고 다음으로 각 인터페이스를 다른 라인에 배치해야 합니다.
```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name),
    KotlinMaker { /*...*/ }
```
