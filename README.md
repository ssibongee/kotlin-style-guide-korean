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
