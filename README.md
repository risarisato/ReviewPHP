## phpの復習
- メソッド
- 継承
- 多様性
- コンストラクタ


## Docker環境
localhost/test.php

```
<?php

/*
 * 命令
 *└─ー 形: オブジェクト.メソッド(パラメータ)
 *  ├─ オブジェクト: document（画面）
 *  ├─ メソッド: write（出力）
 *  └─ パラメータ: 120 * 1.1（計算）
 *       └─ 演算子: *（乗算）
 *
 *  メソッドは、オブジェクトに命令（動作）をさせるもの
 *  関数は、自分で定義して再利用する処理のかたまり
 */


echo nl2br("-----------------------関数メソッド-------------------\n");
// 関数の定義と呼び出し:
// 関数を定義するにはfunctionキーワードを使用します。
// 関数名、引数リスト、関数本体を指定します。
function describe_food($dish) //$dish="焼肉";
{
    echo nl2br("この料理は $dish です。\n");
}
describe_food("焼肉"); // 出力:この料理は焼肉です。


// 関数の中に入る,このとき引数が入り return を実行する
function make_sushi($ingredients, $cooker)
{
    // returnは、値を返して関数を終了します
    return "寿司が作られました。\n" . "使用された食材:$ingredients\n" . "料理人:$cooker\n";
}

$sushi = make_sushi("マグロ、サーモン、アボカド", "寿司職人");
echo nl2br($sushi."\n");

// デフォルト引数:
// デフォルト値を持つ引数は呼び出し時に省略することができます。
function cook_ramen($toppings="チャーシュー")
{
    return "ラーメンが調理されました。トッピング:$toppings";
}

$ramen = cook_ramen(); // デフォルト引数がチャーシュー
echo nl2br($ramen."\n");//出力:ラーメンが調理されました

$ramen = cook_ramen("もやし"); // 引数がもやしに上書きされる
echo nl2br($ramen."\n");//出力:ラーメンが調理されました

// 可変長引数(関数側)＝スプレッド構文(呼び出し側や配列で使う):
function make_tempura(...$ingredients)
{
    $tempura = "天ぷらが作られました。使用食材: ";
    foreach ($ingredients as $ingredient) {
        $tempura .= "$ingredient, ";
    }
    return rtrim($tempura, ", ");
}
$tempura = make_tempura("エビ", "イカ", "ナス");
echo nl2br($tempura."\n");//出力:天ぷらが作られました。使用食材: エビ, イカ, ナス

function tester()
{
    // ③ 関数に入ったら最初にこの行を実行
    echo nl2br("start\n");

    // ④ 次にこの行を実行
    echo nl2br("starterの開始\n");

    echo nl2br("returnのあとは実行されない\n");
    // ⑤ ここで値を返して関数を終了
    return "終了します\n";

    // ⑥ return の後ろなので実行されない
    echo nl2br("ここは実行されない\n");
}

// ① ここで test() を呼び出す
// ② 関数の中に入る
// ⑦ return で返ってきた値を nl2br() で改行表示する
echo nl2br(tester());

function test()
{
    // ③ 関数に入る
    echo nl2br("開始1\n");

    // ④ 次の行を実行
    echo nl2br("ここもされる開始\n");

    // ⑤ 値を返して関数を終了
    return "終了します\n";

    // ⑥ return の後ろなので実行されない
    echo nl2br("ここは実行されない\n");
}

// ① ここで test() を呼ぶ
// ② 関数の中へ入る
$return_value = test();

// ⑦ return で返ってきた値を表示
echo nl2br($return_value);

// ⑦ test() が終わったあと、次の行があればここから再開する

class User
{
    public function hello()
    {
        echo "こんにちは";
    }
}

$user = new User();
$result = $user->hello();
// ここでは echo しているだけ で、return なし！
var_dump($result); // 出力は NULL になる



/*
 * まとめ:
 * - 関数はコードの再利用性を高め、複雑な処理を分割して管理しやすくします。
 * - 引数を使用して関数にデータを渡し、returnを使用して結果を返すことができます。
 * - デフォルト引数や可変長引数を活用することで、柔軟な関数設計が可能になります。
 */

echo nl2br("------------------継承について-------------------------\n");

// 継承についてlesson-17継承
// 継承(Inheritance)の例

//親クラス(スーパークラス)
class Animal
{
    public function makeSound()
    {
        echo nl2br("動物の音を同じメソッド表示：継承\n");
    }
}

// 子クラス(サブクラス→親のAnimalを継承してDogを作る)
class DogExtend extends Animal
{
    public function makeSound()
    {
        echo nl2br("ワンワン！継承\n");
    }
}

// 子クラス(サブクラス→親のAnimalを継承してCatを作る)
class CatExtend extends Animal
{
    public function makeSound()
    {
        echo nl2br("ニャー！継承\n");
    }
}

class ElephantExtend extends Animal
{
    //public function makeSound()
    //{
    //    echo nl2br("パオーン！\n");
    //}   パオーン表示されない
}

// オブジェクトの作成とメソッドの呼び出し
$animal = new Animal();
$dog = new DogExtend();
$cat = new CatExtend();
$elephant = new ElephantExtend();

// 呼び出しているメソッドは全て同じ！
$animal->makeSound(); // 出力: 動物の音を同じメソッド表示
$dog->makeSound();    // 出力: ワンワン！
$cat->makeSound();    // 出力: ニャー！
$elephant->makeSound(); // 出力: 象はmakeSound()が定義無し、パオーン表示されない

/*
 * まとめ:
 * - 継承は、既存のクラスを基に新しいクラスを作成するためのオブジェクト指向の概念です。
 * - 子クラスは親クラスのプロパティやメソッドを引き継ぎ、必要に応じてオーバーライド(上書き)することができます。
 * - 継承を使用することで、コードの再利用性が向上し、クラス間の関係を表現しやすくなります。
 */

echo nl2br("----------------ポリモーフィズム(多態性)-----------------------\n");

class AnimalpolymorphismParent
{
    public function makeSound()
    {
        echo nl2br("わんわん多態性\n");
    }
}

class DogChild extends AnimalpolymorphismParent
{
    public function makeSound()
    {
        echo nl2br("ワンワン！多態性\n");
    }
}

class CatChild extends AnimalpolymorphismParent
{
    public function makeSound()
    {
        echo nl2br("ニャー！多態性\n");
    }
}

// ポリモーフィズムはココで関数を作成する→親クラスを引数する
function animalSound(AnimalpolymorphismParent $animal)
{
    $animal->makeSound(); // 1箇所に関数をまとめられる
}
// オブジェクトの作成
$animal = new AnimalpolymorphismParent();
$dog = new DogChild();
$cat = new CatChild();

// ポリモーフィズムは、同じ関数だが、引数のクラスによって異なる動作違う
// 引数に渡して、1つにまとめることができる
animalSound($animal); // 出力: わんわん多態性
animalSound($dog);    // 出力: ワンワン！多態性
animalSound($cat);    // 出力: ニャー！多態性


/*
 * まとめ:
 * - ポリモーフィズムは、同じインターフェースを持つ異なるクラスのオブジェクトが、同じメソッド呼び出しで異なる動作をする。
 * - これにより、コードの柔軟性と拡張性が向上し、異なるクラスのオブジェクトを同じ方法であつかえる。
 * - ポリモーフィズムは、コードの再利用性を高めることができる。
 */

echo nl2br("------------コンストラクタ：構築する-------------------\n");

class Car
{
    public $color;
    public $model;

    public function __construct (
        $color = "オレンジ色", // 初期値を設定する可能
        $model = "プリウス"
        )
    {
        $this->color = $color;
        $this->model = $model;
    }

    public function getMessage()
    {
        return "私の車は"
               . $this->color
               . " 色の"
               . $this->model
               . " です。";
    }
}

// オブジェクトの作成とメソッドの呼び出し
$carDefault = new Car(); // 初期値
echo nl2br($carDefault->getMessage()."\n");
$car1 = new Car("赤", "スポーツカー"); // 上書き
echo nl2br($car1->getMessage()."\n");
$car2 = new Car("赤"); // 色の赤だで上書き、初期値のプリウス
echo nl2br($car2->getMessage()."\n");

/*
 * まとめ:
 * - コンストラクタは、オブジェクトが作成されるときに自動的に呼び出される特別なメソッドで、オブジェクトの初期化を行います。
 * - コンストラクタは、クラス内で __construct() という名前で定義されます。
 * - コンストラクタは、引数を受け取ることができ、オブジェクトのプロパティを初期化するために使用されます。
 * - コンストラクタを使用することで、オブジェクトの作成と初期化を一元化し、コードの可読性と保守性を向上させることができます。
 */

echo nl2br("------------invoke呼び出す-------------------\n");
class CallableClass
{
    public function __invoke($message)
    {
        echo nl2br("呼び出されました: $message\n");
    }
}
$callable = new CallableClass();
$callable("こんにちは！"); // 出力: 呼び出されました: こんにちは！
/*
 * まとめ:
 * - __invoke() メソッドは、オブジェクトが関数のように呼び出されたときに自動的に実行される特別なメソッドです。
 * - __invoke() を定義することで、オブジェクトを関数のように使用できるようになります。
 * - __invoke() は、引数を受け取ることができ、オブジェクトが呼び出されたときの動作を定義するために使用されます。
 * - __invoke() を使用することで、オブジェクトをより柔軟に扱うことができ、コードの表現力を高めることができます。
 */

echo nl2br("------------デストラクタ：破壊する-------------------\n");
class User
{
    public $name;

    public function __construct($name)
    {
        $this->name = $name;
        echo nl2br("ユーザー {$this->name} が作成されました。\n");
    }

    public function __destruct()
    {
        echo nl2br("ユーザー {$this->name} が破棄されました。\n");
    }
}
$user1 = new User("Alice");
$user2 = new User("Bob");
// オブジェクトを明示的に破棄する
unset($user1); // 出力: ユーザー Alice が破棄されました。
echo nl2br("ユーザー {$user2->name} はまだ存在しています。\n");
// スクリプトの終了時に残りのオブジェクトが破棄される
/*
    * まとめ:
    * - デストラクタは、オブジェクトが破棄されるときに自動的に呼び出される特別なメソッドで、リソースの解放やクリーンアップを行います。
    * - デストラクタは、クラス内で __destruct() という名前で定義されます。
    * - デストラクタは、オブジェクトが明示的に破棄されたときや、スクリプトの終了時に自動的に呼び出されます。
    * - デストラクタを使用することで、オブジェクトが不要になったときにリソースを適切に解放し、メモリリークを防止することができます。
 */

```
