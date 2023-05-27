# 🍓🍌🧃 쥬스 메이커

## 📖 목차
1. [소개](#-소개)
2. [팀원](#-팀원)
3. [타임라인](#-타임라인)
4. [시각화된 프로젝트 구조](#-시각화된-프로젝트-구조)
5. [실행 화면](#-실행-화면)
6. [트러블 슈팅](#-트러블-슈팅)
7. [참고 링크](#-참고-링크)
8. [팀 회고](#-팀-회고)

</br>

## 🍀 소개
훈맹구(`hoon`, `redmango`) 팀이 만든 쥬스 메이커 프로젝트입니다. 첫 화면에서는 현재 가지고 있는 과일과 수량이 나타나며 원하는 쥬스를 선택하여 주문할 수 있습니다. 다음 화면에서는 과일의 재고 관리를 해주는 동작을 수행합니다. 쥬스를 주문하면 알림 창을 통해 쥬스가 나왔다는 것을 사용자에게 알립니다. 재고가 부족하여 만들지 못하는 경우 알림 창에서 바로 재고 관리 화면으로도 넘어갈 수 있습니다.

* 주요 개념: `Initialization`, `Access Control`, `Nested Types`, `Type Casting`, `Error Handling`

</br>

## 👨‍💻 팀원
| redmango | hoon |
| :--------: | :--------: |
| <Img src = "https://hackmd.io/_uploads/HJ2D-DoNn.png" width="200" height="200"> |<Img src="https://hackmd.io/_uploads/HylLMDsN2.jpg" width="200" height="200"> |
|[Github Profile](https://github.com/redmango1447) |[Github Profile](https://github.com/Hoon94) |



</br>

## ⏰ 타임라인
|날짜|내용|
|:--:|--|
|2023.05.08.| - `fruit` 인스턴스 생성을 위한 `Fruit` 클래스 추가 <br> - 쥬스 레시피를 위한 `Recipe` 열거형 추가 |
|2023.05.09.| - 쥬스를 만드는 기능과 쥬스의 재료 부족 시 오류 처리 추가 |
|2023.05.10.| - `Fruit`, `Recipe` 사용자 타입 리팩토링 <br> - `Ingredient` 구조체 추가 | 
|2023.05.11.| - `FruitStore` `struct` 타입으로 변경 <br> - 재료 차감시 발생하는 오류 수정 |
|2023.05.12.| - `decereaseStock` 메서드 수정|
|2023.05.15.| - `alert` 구현 및 `View`와 `ViewController` 연결|
|2023.05.16.| - 에러처리 위치 수정 및 사용자 선택에 따른 데이터 반영을 위해 `UILabel` 및 주문버튼 판단 로직 수정|
|2023.05.17.| - `UILabel`을 하나의 `IBOutlet Collection`으로 수정 및 `fruitStore` 프로퍼티 은닉화|
|2023.05.18.| - 주스 주문 버튼과 `Enum`타입 `Juice`의 매칭을 위해 `CustomButton`클래스 생성 및 활용|
|2023.05.19.| - 네이밍 수정|
|2023.05.22.| - `재고 추가 View`에 `Auto Layout` 적용 <br> - `alert`관련 메서드 하나로 통일|
|2023.05.23.| - 재고 추가 기능을 위한 `UIStepper` 사용 <br> - `FruitStore struct`를 `FruitStore singleton class`로 변경 <br> - `delegate` 패턴을 활용하여 화면 간의 정보 전달|
|2023.05.24.| - `stockManagementViewController`에서 `FruitStore`의 `stockList`를 변경하는 기능 추가 <br> - `touchUpStockStepper` 메서드 내부의 `switch`문 분리|
|2023.05.25.| - `Configurable protocol` 파일 분리 <br> - `Class Diagram` 작성|
|2023.05.26.| - `FruitStore singleton class` 제거|

</br>

## 👀 시각화된 프로젝트 구조

### Diagram
<p align="center">
<img width="800" src="https://hackmd.io/_uploads/HkLt6AhBh.jpg">
</p>

</br>

## 💻 실행 화면

| 과일 쥬스 주문하기 |
|:--------:|
|<img src="https://hackmd.io/_uploads/By1dkl0B3.gif">|

| 화면 전환하기 |
|:--------:|
|<img src="https://hackmd.io/_uploads/H1aDve0r3.gif">|

| 과일 재고 추가하기 |
|:--------:|
|<img src="https://hackmd.io/_uploads/HyecDlAH2.gif">|


</br>

## 🧨 트러블 슈팅

1️⃣ **`Fruit` 사용자 타입 생성** <br>
-
🔒 **문제점** <br>

- 다양한 종류의 과일 예제들이 미션에서 주어졌습니다. 주어진 과일에 대해 이름과 수량을 저장하고 있어야 했기 때문에 `class` 타입을 활용하여 `Fruit`을 생성하였습니다.

    ```swift
    class Fruit {
        var name: String
        var quantity: Int

        init(name: String, quantity: Int) {
            self.name = name
            self.quantity = quantity
        }
    }
    ```

🔑 **해결방법** <br>

- 처음 생성한 `Fruit`은 수량을 의미하는 `quantity` 프로퍼티를 가지고 있었습니다. 하지만 과일이라는 네이밍의 클래스 안에 과일의 이름, 색, 당도 등의 프로퍼티는 가능하지만 과일 객체 자체가 자신의 수량을 가지고 있다는 점이 객체지향적 관점에서는 어색하다는 말씀을 듣고 이번 과제를 하며 다시 객체에 대해 생각해 보는 시간이 되었습니다.

    ```swift
    enum Fruit: CaseIterable {
        case strawberry
        case banana
        case pineapple
        case kiwi
        case mango
    }
    ```
    `Fruit`에서 어색한 `quantity`를 빼고 위와 같이 `enum`으로 재정의 하였습니다.


<br>

2️⃣ **과일 종류에 따른 초기화 방법** <br>
-
🔒 **문제점** <br>

- `FruitStore`에 생성한 `stockList` 프로퍼티에 각각의 과일 초기 수량을 저장하기 위해 `dictionary` 타입을 사용하였습니다. 과일 초기 값이 10이라는 요구사항을 지키기 위해 프로퍼티에 기본 값을 할당하려 했지만 만약 초기 값이 변경 된다면 `dictionary`의 특성과 `Fruit`의 갯수에 따라 수정하기가 힘들수도 있다고 판단 되었습니다. 그에따라 처음엔 메서드를 만들어 사용하려 했습니다.


🔑 **해결방법** <br>

- 
    ```swift
    init(stockQuantity: Int = 10) {
        for fruit in Fruit.allCases {
            stockList[fruit] = stockQuantity
        }
    }
    ```
    하지만 메서드를 만들고 호출하여 `stockList`를 채우기보다는 `init` 함수를 사용하여 `FruitStore`의 인스턴스(객체)를 생성할 때 각각 과일에 대한 값들을 추가하도록 하였습니다. `init` 함수에서 `for`문을 활용하여 `Fruit`에 들어있는 과일들을 꺼내오기 위해 `CaseIterable` 프로토콜을 채택하였습니다.


<br>

3️⃣ **`enum Juice` 활용 방법** <br>
-
🔒 **문제점** <br>
- 처음엔 `Raw Values`를 사용하려 했으나 사용 시 정확히 무엇을 뜻하는지 모른다는 조언을 듣고 `Associated Values`를 사용하기로 했습니다. 하지만 그 결과 `JuiceMaker`내부에 스위치 문을 사용하게 되었고 반복되는 코드의 양이 너무 많아 가독성을 떨어뜨리게 되었습니다.

    ```swift
    func makeJuice(with recipe: Recipe) {
        let fruitStore: FruitStore = FruitStore()

        switch recipe {
        case .strawberryJuice(strawberry: let quantity):
            fruitStore.changeStock(of: fruitStore.strawberry, by: quantity)
        case .bananaJuice(banana: let quantity):
            fruitStore.changeStock(of: fruitStore.banana, by: quantity)
        case .kiwiJuice(kiwi: let quantity):
            fruitStore.changeStock(of: fruitStore.kiwi, by: quantity)
        case ...
        }
    }
    ```

🔑 **해결방법** <br>

 - 열거형 안에서 연산 프로퍼티 사용이 가능하다는 것을 알게 되었습니다. 초기엔 스위치문에 튜플,배열 등의 자료형을 사용하여 결과를 리턴 받아 사용했으나 `Ingredient`라는 타입을 만들어 보라는 조언에 따라 아래와 같이 코드를 생성 및 수정하여 활용했습니다.
    
    ```swift
    struct Ingredient {
        let name: Fruit
        let quantity: Int
    }
    ```

    ```swift
    enum Juice {
        case...

        var recipe: [Ingredient] {
            switch self {
            case .strawberryJuice:
                return [Ingredient(name: .strawberry, quantity: 16)]
            case...
            }
        }
    }
    ```
    
    ```swift
    mutating func makeOrder(juice: Juice) {
        do {
            for ingredient in juice.recipe {
                try fruitStore.checkStock(witch: ingredient.name, by: ingredient.quantity)
            }
            
            try juice.recipe.forEach { fruitStore.decreaseStock(witch: $0.name, by: $0.quantity) }
        } catch FruitStoreError.outOfStock(let fruit) {
            print("\(fruit)의 재고가 부족합니다.")
        } catch {
            print("알 수 없는 오류 발생.")
        }
    }
    ```
    
    또한 `Ingredient`타입을 `FruitStore`내 메서드에 매개변수로 받아옴으로써 `JuiceMaker`는 물론이고 `FruitStore`내부 메서드들의 코드가 간소화되고 가독성이 높아졌습니다.


<br>

4️⃣ **`Ingredient` 타입 선언 위치** <br>
-
🔒 **문제점** <br>
 
- `Ingredient` 타입을 처음에는 `Juice` 타입 안에 `Nested Type`으로 생성하였습니다. 생성을 하고 사용을 하다 보니 저희의 코드에서는 `FruitStore`에 있는 메서드인 `decreaseIngredient`에서 다음과 같이 사용하게 되었습니다.
    ```swift
    func decreaseIngredient(with recipe: [Juice.Ingredient] ) throws { ... }
    ```
    여기서 `FruitStore`가 어떤 쥬스를 만드는지에 대해 알 필요가 있을까라는 의문이 들었습니다. 예를 들면 `FruitStore`에서는 **딸기 쥬스를 만들기** 위한 딸기 10개를 감소한다가 아닌 단순하게 **무엇을 만들지는 모르겠지만** 딸기 10개를 감소한다가 더 올바른 표현이지 않을까라는 생각을 가졌습니다. 이러한 생각 때문에 `Ingredient` 타입이 `Juice` 타입 내부에 있는 것이 아닌 외부에 존재해야 한다고 생각하였습니다. 이를 수정하여 다음과 같이 메서드를 선언하였습니다.
    ```swift
    func decreaseIngredient(with recipe: [Ingredient] ) throws { ... }
    ```

🔑 **해결방법** <br>

- `Ingredient` 타입은 `name`과 `quantity`를 프로퍼티로 가지고 있습니다. `FruitStore` 타입 안에 재고를 감소시키는 메서드에서 `Ingredient`라는 네이밍의 매개변수가 필요한지에 대해서 다시 한번 생각해 보게 되었습니다. 재료가 무엇인지를 알 필요 또한 없다고 생각이 들었고 처음 받아오는 파라미터에서 `name`과 `quantity`로 나누어서 전달 인자를 받는 방법으로 수정을 하였습니다.

    ```swift
    mutating func decreaseStock(witch fruit: Fruit, by quantity: Int) { ... }
    ```
    
    위와 같이 코드를 수정하고 나서 보면 `Ingredient`는 더 이상 사용하지 않는 타입이 되었습니다. 이를 통해 `Juice` 타입 안에 다시 `Nested Type`으로 `Ingredient`을 선언하였습니다.


<br>

5️⃣ **여러 `UIButton`들을 하나의 `@IBAction`으로 묶기** <br>
-
🔒 **문제점** <br>
- 쥬스를 주문하는 버튼이 각각의 쥬스 종류만큼 개별적으로 존재했습니다. 모든 주문 버튼에 관련하여 각각 `@IBAction`을 생성하는 경우 아래와 같이 중복되는 코드의 양이 무척 많았습니다.

    ```swift
    @IBAction func touchUpStrawberryJuiceOrderButton(_ sender: UIButton) { ... }
    @IBAction func touchUpBananaJuiceOrderButton(_ sender: UIButton) { ... }
    @IBAction func touchUpPineappleJuiceOrderButton(_ sender: UIButton) { ... }
    @IBAction func touchUpKiwiJuiceOrderButton(_ sender: UIButton) { ... }
    @IBAction func touchUpMangoJuiceOrderButton(_ sender: UIButton) { ... }
    @IBAction func touchUpStrawberryBananaJuiceOrderButton(_ sender: UIButton) { ... }
    @IBAction func touchUpMangoKiwiJuiceOrderButton(_ sender: UIButton) { ... }
    ```

🔑 **해결방법** <br>
- 이러한 부분을 수정하기 위해 하나의 `@IBAction`에서 버튼을 구분 지어 각각의 버튼에 맞는 동작을 수행하도록 수정하였습니다.
    
    ```swift
    @IBAction func touchUpOrderButton(_ sender: UIButton) { ... }
    ```
    위와 같이 하나의 `@IBAction`에서 각각의 버튼을 구분하기 위해서는 이를 구분하기 위한 식별자가 필요했습니다. `UIButton`의 `tag`와 `title` 프로퍼티를 사용하여 식별자 역할을 할 수 있었습니다. 두 방법에 대해 다음과 같이 코드로 표현하였습니다.
    - `tag` 사용

        ```swift
        @IBAction func touchUpOrderButton(_ sender: UIButton) {
            try juiceMaker.makeOrder(sender.tag)    
        }
        ```
        
        `tag`를 사용하여 해결을 한 경우 각각의 버튼에서 가지고 있는 프로퍼티의 `tag`값을 모두 개별적으로 지정해 주어야 한다는 점에서 코드의 수정이 필요했습니다. 또한 `tag`는 기본값으로 0을 가지고 있기 때문에 새로운 버튼을 추가하고 개발자가 `tag`를 수정하지 않을 시 같은 `tag` 값을 갖는 문제가 발생하였습니다.
        
    - `title` 사용
    
        ```swift
        @IBAction func touchUpOrderButton(_ sender: UIButton) {
            guard let title = sender.titleLabel?.text,
                  let juice = Juice(rawValue: title)
            else {
                return
            }

            try juiceMaker.makeOrder(juice)
        }
        ```
        
        `title` 사용 시 버튼에 대한 기본 네이밍의 양식이 같다면 추가 수정 없이 Juice의 원시 값을 수정하여 매칭을 시킬 수 있었습니다. 이렇게 된다면 버튼이 추가될 때 `Juice`의 원시 값만 추가하여 해당 버튼의 `title`과 같은 값으로 맞춰주면 되었습니다.
        
        위의 두 경우를 비교하여 생각하였을 때 `title`을 사용하는 방식이 `tag`를 활용하는 방법보다 새로운 버튼이 추가되었을 때 더 적은 수정을 필요로 하고 혹시 모를 에러(ex: 버튼 추가 후 `tag`미 수정 등)를 미연에 방지하기 때문에 최종적으로 `title`을 활용하기로 결정하여 문제를 해결하였습니다.


<br>

6️⃣ **`Juice`와 쥬스 주문 버튼의 매칭** <br>
-
🔒 **문제점** <br>
- 처음엔`Juice`의 `rawValue`와 `UIButton`의 `titleLabel`을 가져와 매칭 시켰으나 아래와 같은 리뷰를 받고 고민해 본 결과 열거형의 원시값을 사용하는 것이 아닌 다른 방법으로 문제를 해결해야겠다고 생각하였습니다.
  > Juice의 rawVaule가 titleLabel가 무슨 연관성이 있는지 잘 모르겠습니다. by som
 
    ```swift
        @IBAction func touchUpOrderButton(_ sender: UIButton) {
            guard let title = sender.titleLabel?.text,
                let juice = Juice(rawValue: title)
            else {
                return
            }
            ...
        }
    ```


🔑 **해결방법** <br>
- `switch`문 활용
    우선 `switch`문을 활용할 수 있게 적절한 값이 필요하다는 판단에 `Enum`타입의 `Juice`에 아래와 같이 연산 프로퍼티를 선언하였습니다.
    
    ```swift
    var name: String {
        switch self {
        case .strawberryJuice:
            return "strawberryJuice"
        case .bananaJuice:
            return "bananaJuice"
        case...
        }
    }
    ```
    
    이후 `UIButton`의 식별자로 활용할 만한 요소가 무엇이 있을까 고민하다가 `accessibilityIdentifier` 값을 사용하기로 결정하고 아래와 같이 `IBOutlet Collection`이용해 이전에 생성한 `Juice.name`값을 순차적으로 넣어줬습니다.
    
    ```swift
     private func fillJuiceButtonIdentifier() {
        for index in orderJuiceButtonCollection.indices {
            orderJuiceButtonCollection[index].accessibilityIdentifier = Juice.allCases[index].name
        }
    }
    ```
    
    다음으로는 저희가 의도한 대로 받아온 `UIButton`의 `accessibilityIdentifier`값을 `switch`문에 사용하여 `Juice`와 매칭하였고, 나온 반환값을 `juiceMaker.makeOrder()` 메서드의 매개변수로 넣어주었습니다.
    
    ```swift
    private func matchJuiceMenu(with buttonIdentifier: String) throws -> Juice {
        switch buttonIdentifier {
        case "strawberryJuice":
            return .strawberryJuice
        case "bananaJuice":
            return .bananaJuice
        case...
        default:
            throw JuiceError.outOfMenu
        }
    }

    @IBAction func touchUpOrderButton(_ sender: UIButton) {
        guard let buttonIdentifier = sender.accessibilityIdentifier else { return }
        
        let juice: Juice = matchJuiceMenu(with: buttonIdentifier)
        juiceMaker.makeOrder(juice)
        ...
    }
    ```
    
- `customIdentifier`를 만들어 사용
    "`Button`에 `Juice`타입을 만들어 줄 수는 없을까?"라는 고민을 시작으로 별도의 타입을 만들어 상속시켜 사용해 보자는 결론을 내렸습니다. 그에 따라 아래와 같이 `UIButton`을 상속받은 `CustomButton`을 만들어 프로퍼티로 `Juice` 타입의 `customIdentifier`를 선언하였습니다.
    
    ```swift
    final class CustomButton: UIButton {
        var customIdentifier: Juice?
    }
    ```
    
    이후 모든 주스 주문 버튼에 `Juice`를 넣어줘야 하니 각각 넣어주는 건 추후 확장성 등을 고려해 비효율적이라는 판단에 `IBOutlet collection`와 `CaseIterable`을 활용하기로 결정했습니다. 물론 그전에 StoryBoard의 주문 버튼들의 `CustomClass` 설정을 일일이`CustomButton`으로 변경해 주는 과정이 필요했습니다. 
    
    이 과정에서 휴먼 에러가 발생하진 않을까 고민해 봤지만 이 과정을 실행하지 않을 경우 `CustomButton`타입인 `IBOutlet collection`와 이벤트 시 실행되는 메서드에 등록되지 않으니 체크가 반강제되고, 혹시 아예 과정 자체를 깜빡하는 경우를 생각해 봐도 발생할 수 있는 경우의 수는 `아무것도 실행되지 않음` or `Juice.allCases[index]`의 `indexOverError`이 2가지로 추측된다고 결론이 났습니다. 후자의 `indexOverError`의 경우 `for`문의 반복횟수를 `IBOutlet collection`를 기준으로 할 경우 방지할 수 있다고 판단하여 아래와 같이 코드를 작성 하였습니다.(`orderJuiceButtonCollection`과 `Juice`의 순서는 미리 맞춰뒀습니다.)

    ```swift
    private func fillJuiceButtonCustomIdentifier() {
        for index in orderJuiceButtonCollection.indices {
            orderJuiceButtonCollection[index].customIdentifier = Juice.allCases[index]
        }
    }
    ```
    
    마지막으로 버튼 이벤트 발생시 해당 버튼의 `customIdentifier`를 받아와 바로 메서드의 매개변수로 넣어주었습니다.
    
    ```swift
    @IBAction func touchUpOrderButton(_ sender: CustomButton) {
        guard let juice = sender.customIdentifier else { return }
        
        juiceMaker.makeOrder(juice)
    }
    ```


<br>

7️⃣ **`AlertAction handler` 화면 전환 방법** <br>
-
🔒 **문제점** <br>
- `재고 수정`을 누를 경우 `Segue`를 사용해`Present Modally` 방식으로 재고 수정 `viewController`와 연결해 줬습니다. `Alert`창에서 "예"를 누를 경우에도 `AlertAction handler`를 활용해 같은 재고 수정 `viewController`로 화면전환을 해줘야 하기에 처음엔 아래와 같이 `viewController`의 `identifierID`를 활용해 인스턴스화하여 `present` 해주는 방식으로 화면 전환을 하였습니다.

    ```swift
    guard let nextView = self.storyboard?.instantiateViewController(identifier: "identifierID") else { return }
    self.present(nextView, animated: true)
    ```

🔑 **해결방법** <br>
- 앞서 스토리보드에서 사용한 기존의 `Segue`를 어떻게 활용할 방법이 없을까 하고 고민이 들었고 결국 `performSegue`을 활용해 아래와 같이 해결했습니다.
    
    ```swift
    let confirmAction = UIAlertAction(title: "예", style: .default) { _ in
        self.performSegue(withIdentifier: "goToStockViewController", sender: nil)
    }
    ```


<br>

8️⃣ **`View Controller`는 `Fruit`의 종류를 알아야 하는가?** <br>
-
🔒 **문제점** <br>
- 뷰 컨트롤러에서 뷰에 있는 각각의 과일에 대한 수량을 나타내주는 UILabel을 초기화하기 위해 아래와 같은 메서드를 사용하였습니다.

    ```swift
    private func changeStockLabel() {
        for (fruitStockLabel, fruit) in zip(fruitStockLabels, Fruit.allCases) {
            fruitStockLabel.text = juiceMaker.showRemainStock(of: fruit)
        }
    }
    ```
    
    `changeStockLabel` 메서드를 보면 `Fruit`의 종류를 `showRemainStock`의 인자로 전달하고 있습니다. 프로젝트를 진행하며 가장 많이 고민했던 점 중에 하나가 바로 객체의 관점에 대한 이해였고 뷰 컨트롤러 또한 쥬스의 종류까지만 알고 내부에서 사용하는 쥬스의 재료에 대한 `Fruit` 타입에 대해 알고 있지 않아도 되겠다는 생각을 가졌습니다.

🔑 **해결방법** <br>
- 뷰 컨트롤러가 `Fruit`의 종류는 모르되 뷰의 `UILabel`에 입력할 수량에 대한 정보는 있어야함으로 `Array<Int>` 타입으로 수량에 대한 정보를 반환하였습니다. 배열 안에 있는 원소의 순서는 `Fruit`에 선언되어 있는 과일 종류의 순서에 맞추었습니다. 또한 기존에 사용하던 `changeStockLabel`명보다는 뷰 컨트롤러의 관점에서 `UILabel`을 채운다는 생각으로 `fillStockLabel`로 변경하였습니다.

    ```swift
    // class JuiceOrderViewController
    private func fillStockLabel() {
        let currentStockList: [String] = juiceMaker.showRemainStock()
        
        for index in fruitStockLabelCollection.indices {
            fruitStockLabelCollection[index].text = currentStockList[index]
        }
    }
    ```

    ```swift
    // struct JuiceMaker
    func showRemainStock() -> [String] {
        return fruitStore.getRemainStock()
    }
    ```
    
    ```swift
    // struct FruitStore
    func getRemainStock() -> [String] {
        var fruitStockList: [String] = []
        
        for fruit in Fruit.allCases {
            let currentStock: Int = stockList[fruit] ?? 0
            fruitStockList.append(String(currentStock))
        }
        
        return fruitStockList
    }
    ```
    
    위와 같이 코드를 수정함으로써 뷰 컨트롤러는 `Fruit`을 알 필요가 없어졌고 또한 `showRemainStock`을 통해서 `getRemainStock` 메서드에 접근하기 때문에 `FruitStore`까지도 은닉화를 시킬 수 있었습니다.


<br>

9️⃣ **`delegate` 패턴을 사용하여 이전 화면의 `UILabel` 업데이트** <br>
-
🔒 **문제점** <br>
- `StockManagementViewController`에서 재고에 추가된 내용을 `FruitStore`의 `stockList`에 저장하였습니다. `JuiceOrderViewController`의 화면에서 `StockManagementViewController`로 전환할 때 `present`를 사용하여 전환하였기 때문에 다시 이전 화면인 `JuiceOrderViewController`로 변경 시 `View State Method`의 `viewWillAppear` 메서드가 다시 호출되지 않는다는 문제점이 있었습니다. `modalPresentationStyle`을 `.fullScreen`로 설정해 주어야 `viewWillAppear` 메서드가 다시 호출되어 그 안에서 `UILable` 값을 변경해 줄 수 있었습니다.

🔑 **해결방법** <br>
- 문제를 해결하고자 이전 화면으로 돌아가기 전 `StockManagementViewController` 화면의 `viewWillDisappear` 메서드에서 `delegate` 패턴을 활용하여 이전 화면의 `UILabel` 값을 다시 입력하도록 수정하였습니다.
    
    ```swift
    // JuiceOrderViewController
    protocol Configurable {
        func assignLabelText()
    }

    extension JuiceOrderViewController: Configurable {
        func assignLabelText() {
            configureStockLabel()
        }
    }

    final class JuiceOrderViewController: UIViewController {
        ...
        
        override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
            guard let stockManagementViewController =
                    segue.destination as? StockManagementViewController
            else {
                return
            }

            stockManagementViewController.configurationDelegate = self
        }
        
        ...
    }
    ```
    ```swift 
    // StockManagementViewController
    final class StockManagementViewController: UIViewController {
        ...
        
        var configurationDelegate: Configurable?   
        
        override func viewWillDisappear(_ animated: Bool) {
            super.viewWillDisappear(animated)
            changeStockList()
            configurationDelegate?.assignLabelText()
        }
        
        ...
    }
    ```


<br>

🔟 **`StockManagementViewController`에서 `FruitStore class instance` 사용** <br>
-
🔒 **문제점** <br>
- 재고 추가 화면인 `StockManagementViewController`에서도 `FruitStore`의 프로퍼티인 `stockList`에 대해서 접근하여 재고 추가에 대한 처리를 진행해야 했습니다. 현재 사용 중인 `JuiceOrderViewController`와 `StockManagementViewController` 모두 같은 값을 가지고 있는 `stockList`를 참조함으로써 화면 간에 데이터 전달이 아닌 공유를 하면 좋겠다는 판단에 싱글톤 클래스로 선언하였습니다.

    ```swift
    class FruitStore {
        static let shared: FruitStore = FruitStore()
        private var stockList: [Fruit: Int] = [:]

        private init(stockQuantity: Int = 10) {
            Fruit.allCases.forEach { stockList[$0] = stockQuantity }
        }

        ...
    }
    ```
    
    하지만 싱글톤 패턴을 사용하면 `thread unsafe` 문제와 싱글톤 객체의 변경이 일어나면 해당 객체를 활용하는 뷰의 수정이 연속적으로 일어나야 하는 문제가 있었습니다. 즉, `SOLID 원칙`의 개방-폐쇄 원칙을 지키지 않는다는 문제가 있었습니다. 

🔑 **해결방법** <br>
- 싱글톤 패턴을 사용하지 않고 첫 화면인 `JuiceOrderViewController`에서 사용하는 `FruitStore` 인스턴스를 다음 화면인 `StockManagementViewController`에 매개변수로 넘겨주었습니다. `class` 타입으로 선언한 `FruitStore`이기 때문에 같은 인스턴스를 참조할 거라고 생각했습니다. 결과적으로`StockManagementViewController`에서 변경한 값은 `JuiceOrderViewController`에도 같이 적용되어 변경된 값을 확인할 수 있었습니다.


<br>

## 📚 참고 링크
- [🍎Apple Docs: Displaying and managing views with a view controller](https://developer.apple.com/documentation/uikit/view_controllers/displaying_and_managing_views_with_a_view_controller)
- [🍎Apple Docs: UIViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller)
- [🍎Apple Docs: Modality](https://developer.apple.com/design/human-interface-guidelines/modality)
- [🍎Apple Docs: Using Delegates to Customize Object Behavior](https://developer.apple.com/documentation/swift/using-delegates-to-customize-object-behavior)
- [🍏Apple Archive: Managing the Lifetimes of Objects from Nib Files](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/LoadingResources/CocoaNibs/CocoaNibs.html#//apple_ref/doc/uid/10000051i-CH4-SW6)
- [🍏Apple Archive: Outlets](https://developer.apple.com/library/archive/documentation/General/Conceptual/CocoaEncyclopedia/Outlets/Outlets.html)
- [🍏Apple Archive: Singleton](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Singleton.html)
- [🍏Apple Archive: Delegation](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Delegation.html)
- [🍏Apple Archive: Auto Layout](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/index.html)
- [📼Apple WWDC: Understanding Swift Performance](https://developer.apple.com/videos/play/wwdc2016/416/)
- [📙stackOverflow: IBOutlet Collection](https://stackoverflow.com/questions/43398329/swift-iboutlet-collections-and-retain-cycle-safety)
- [📘blog: Alert](https://peppo.tistory.com/29)
- [📘blog: IBOutlet Collections](https://skytitan.tistory.com/579)
- [📘blog: Tag](https://g1embed.tistory.com/8)
- [📘blog: Accessibility Identifier](https://mildwhale.github.io/2019-12-26-uitesting-tip-and-tricks/)
- [📘blog: IBOutlet Reference Counting](https://co-dong.tistory.com/60)
- [📘blog: Auto Layout](https://velog.io/@eddy_song/ios-auto-layout-1)
- [📘blog: View Controller 간 데이터 전달](https://velog.io/@nnnyeong/iOS-VC-%EA%B0%84-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EB%8B%AC-%EB%B0%A9%EB%B2%95)
- [📘blog: UML Class Diagram](https://www.nextree.co.kr/p6753/)


</br>

## 👥 팀 회고
- [팀 회고 링크](https://github.com/redmango1447/ios-juice-maker/blob/main/%ED%8C%80%ED%9A%8C%EA%B3%A0.md)
