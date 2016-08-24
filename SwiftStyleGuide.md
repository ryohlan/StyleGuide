#[WIP] Swift Style Guide

# Style
基本的には可読性のための規約.
Must, Should

## プロパティ
### 変更可能性が無いプロパティはlet宣言する
Xcodeだとlintが警告を出る

### 1行に2つ以上の宣言をしない
```swift
//Good
let text: String
let message: String

//Bad
let text: String, message: String
```

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
let kind: Kind = .Animal
kind = .Plant

//Bad
let text: String = "text"
let kind: Kind = Kind.Animal
kind = Kind.plant
```
### Arrayの定義・初期化
```swift
//Good
var messages = [String]()
var messages = ["text", "message"]
var messages: [String]? = nil

//Bad
var messages = Array<String>()
var messages = Array<String>(arrayLiteral: "text", "message")
var messages: Array<String>? = nil
```

### インスタンスプロパティに内部からアクセスする際にSelfは付けない
これは賛否ある
```swift
//Good
override func viewDidLoad() {
    super.viewDidLoad()
    model = Model()
}

//Bad
override func viewDidLoad() {
    super.viewDidLoad()
    self.model = Model()
}

```
### Computed valueのは省略できるものは省略する
```swift
//Good
var number: Int { return 40 }//getだけの場合は省略できる

//Bad
var number: Int {
  get {
    return 40
  }
}
```

## オプショナル
### Implicitly Unwrapped Optional型は必ず初期化がされる場合にのみ使用可
極力避ける

### Fource Unwrappは使わずOptional Bindingを使う
```swift
//Good
let text: String? = nil
...

if let text = text {
  ...
}

guard let text = text else { return }

let text = text ?? ""

//Bad
let text = text!
```

### バインド先はバインド元と同じ名前にする
```swift
let message: String = nil

//Good
guard let message = message else { return }

//Bad
guard let msg = message else { return }
```

### if let より gurad を用いて早期リターンを使う
```swift
//Good
guard let text = text else { return }
setText(text)

//Bad
if let text = text {
  setText(text)
}
```

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

### @noescape以外のクロージャ無いのself参照は循環参照を避けるため[weak self]を宣言し、`self`にguard文でバインドする。ただし処理が1行で済む場合はself?を参照してもよい
```swift
//Good
button.rx_tap.subscribeNext { [weak self] _ in guard let `self` = self else { return }
  ...
  ...
  ...
}
button.rx_tap.subscribeNext { [weak self] _ in self?.text = "tap" }

//Bad
button.rx_tap.subscribeNext { _ in self.text = "tap" }
button.rx_tap.subscribeNext { [weak self] in
  if let `self` = self {
    ...
  }
 }
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

## Enum
### パスカルケースで記述
```swift
//Good
enum King {
  case Animal, Plant
}

//Bad
enum Kind {
  case animal, plant
}
```

## Protocol
### Extensionを利用する
```swift
//Good
class ViewController: UIViewController {
  ...
}

extension ViewController: UITableViewDataSource {
  ...
}

//Bad
class ViewController: UIViewController, UITableViewDataSource {
  ...
}
```

## Tuple
### 名前を付ける
```swift
//Good
let tpl = (name: "namae", size: 32)
typealias tpl = (name: String, size: Int)

//Bad
let tpl = ("name", 32)
typealias tpl = (String, Int)
```
