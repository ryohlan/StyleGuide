# Style
基本的には可読性のための規約

## プロパティ
### 変更可能性が無いプロパティはlet宣言する
Xcodeだとlintが警告を出します

### セミコロンはつけない
```swift
//Good
let text = "text"

//Bad
let text = "text";
```

### タブを半角スペース4つに
XcodeやAtomなどの設定を合わせる

### プロパティは下に空行を入れない
```swift
//Good
let text = "text"
let number = 10

//Bad
let text = "text"

let number = 10

```
### 型宣言はコロンの右側にスペース、等号の左右にスペースを入れる
```swift
//Good
var text: String? = nil

//Bad
var text:String?=nil
var text : String? =nil
```

### 外部からアクセスが必要ないプロパティ、メソッドはprivateにする
```swift
//Good
private let innerValue = 10

private func countUp(){
  ...
}
```

### プロパティの順序
* @付きプロパティ
* let
* var
* weak var
* computed var
* lazy var

### 型推論が有効な場合は型宣言を省略する
```swift
//Good
let text = "text"
let kind = Kind.Animal
kind = .Plant

//Bad
let text: String = "text"
let kind: Kind = Kind.Animal
kind = Kind.plant
```


## オプショナル
###


## メソッド
### メソッドは下に空行を1行入れる
```swift
//Good
func run() {
  ...
}

func alert() {
  ...
}


//Bad
func run() {
  ...
}
func alert() {
   ...
 }
```

### メソッドの返り値の定義はスペースを入れる
``` swift
//Good
func run() -> Int {
  ...
}

//Bad
func run()->Int{
  ...
}
```

### メソッドを1行で書いてはならない
```swift
//Good
func func() {
  ...
}

//Bad
func run() { ... }
```


## クロージャ
### 引数、return, 引数が1つだけのクロージャの場合の丸括弧を省略できる場合は省略する
```swift
//Good
items.map { $0.kind }

//Bad
items.map({ $0.kind })
items.map{ kind in return kind}
```

### 使用しない引数は_（アンダースコア）を使う
```swift
//Good
button.rx_tap.subscribeNext { _ in print("tap") }

//Bad
button.rx_tap.subscribeNext { button in print("tap") }
```

### @noescape以外のクロージャ無いのself参照は循環参照を避けるため[weak self]を宣言する
```swift

```

## Naming
### キャメルケースを使用する
```swift
//Good
class MyItem {}
struct MyItem {}
var itemsCount = 10
func getItemsCount() -> Int {
  ...
}

//Bad
class my_item{}
class My_item {}
var items_count = 10
func get_itemsCount() -> Int {
  ...
}
```

### 一般的でない略語を使わない
```swift
//Good
let errorMessage = errorResponse.message

//Bad
let em = errorResponse.message
```
