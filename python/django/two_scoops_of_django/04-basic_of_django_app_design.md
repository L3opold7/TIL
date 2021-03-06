장고 앱 디자인의 기본
===

## 1. 장고 앱 디자인의 황금률

> "좋은 장고 앱을 정의하고 개발하는 것은 더글라스 맥얼로이의 유닉스 철학을 따르는 것이다. 한번에 한 가지 일을 하고 그 한 가지 일을 매우 충실히 하는 프로그램을 짜는 것이다." - 제임스 베넷(장고 코어 개발자 이자 릴리즈 매니저)

핵심은 **각 앱이 그 앱의 주어진 임무에만 집중할 수 있어야 한다는 것이다**.

부가적으로 그 앱을 설명하기 위해 '그리고/또한' 이라는 단어를 한 번 이상 사용한다면 그 앱은 나눌 필요가 있는 앱이다.

## 2. 장고 앱 이름 정하기

명료한 이름으로 짓는 것이 좋다.

가능하면 한 단어로 된 이름을 이용한다.

앱의 이름은 앱의 중심이 되는 모델 이름의 복수 형태가 되어야 한다.

물론 예외는 존재한다. e.g. "blog"

단순히 앱의 메인 모델만을 고려하지 않도록 한다.

이름을 정할 때 URL 이 어떻게 될 지도 고려하면 좋다.

PEP-8 규약에 맞게 import 될 수 있는 이름을 이용하도록 한다.


## 3. 확신 없이 앱을 확장하지 않는다.

너무 심오하게 고민하지는 말자.

앱들을 될 수 있으면 작게 유지하려고 하자.

거대한 크기의 앱 두세 개를 구성하는 것보다 작은 앱 여러 개를 구성하는 것이 훨씬 나은 구성이다.

## 4. 앱 안에는 어떤 모듈이 위치하는가?

### 4-1. 공통 모듈

```
__init__.py
admin.py
forms.py
management/
migrations/
models.py
templatetags/
tests/
urls.py
views.py
```

이 규칙을 반드시 따라야 하는 것은 아니지만 따르는 게 자신 스스로를 위해서라도 좋다.

### 4-2. 비공통 모듈

```
behaviors.py
constants.py
context_processors.py
decorators.py
db/
exceptions
fields.py
factories.py
helpers.py
managers.py
middleware.py
signals.py
utils.py
viewmixins.py
```

behaviors.py: 모델 믹스인 위치에 대한 옵션

constants.py: 앱 레벨에서 이용되는 세팅을 저장하는 장소의 이름으로 잘 지어진 이름이라 할 수 있다. 하나의 앱에 다양한 세팅이 있다면 이를 각 모듈로 분리하여 놓는 것이 명확성을 위해서 좋을 것이다.

decorators.py: 데코레이터가 존재하는 곳이다.

db/: 여러 프로젝트에서 이용되는 커스텀 모델이나 컴포넌트

fields.py: 폼 필드 이용에 쓰인다. 하지만 때때로 db/ 패키지 생성으로도 충분하지 못한 필드가 존재할 때 이용되기도 한다.

factories.py: 테스트 데이터 팩토리 파일이다.

helpers.py: 헬퍼 함수다. 뷰와 모델을 가볍게 하기 위해 뷰와 모델에서 추출한 코드를 저장하는 장소다. 

managers.py: models.py 가 너무 커질 경우, 일반적인 해결책으로 커스텀 모델 매니저가 여기로 이동된다.

signals.py: 커스텀 시그널을 제공하는 것에 대한 대안으로 커스텀 시그널을 넣기에 유용한 공간이다.

utils.py: helpers.py 와 같은 기능이다.

viewmixins.py: 뷰 믹스인을 이 모듈로 이전함으로써 뷰 모듈과 패키지를 더 가볍게 할 수 있다.

## 5. 요약

장고 앱은 그 앱 자체가 지닌 한 가지 역할에 초점이 맞추어져야 하며 단순하고 쉽게 기억되는 이름을 가져야 한다.

기능이 너무 복잡하면 다른 여러 개의 작은 앱으로 나누어야 한다.
