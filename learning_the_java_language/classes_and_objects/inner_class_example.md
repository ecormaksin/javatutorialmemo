# Inner Class Example(インナー クラスの例)

インナー クラスの使い方を見るために、まず配列を考えてみる。次の例では、配列を作成し、整数値を格納し、偶数インデックスの値のみを昇順で出力する。

`DataStructure.java`の例は、以下のもので構成されている。

- `DataStructure` アウター クラス
  - コンストラクター
    - 連続した整数を設定した配列を持つ`DataStructure`のインスタンスを生成する。
  - メソッド
    - 偶数インデックス値を持つ配列の要素を出力する。（訳時補足: 偶数インデックスには偶数が格納されているので、偶数を出力することと同義。）
- `EvenIterator` インナー クラス
  - `Iterator<Integer>`インターフェイスを継承した`DataStructureIterator`インターフェイスを実装する。
  - イテレーターはデータ構造を一通り処理するのに使われる。典型的に次のメソッドを持つ。
    - 最後の要素か検証する。
    - 現在の要素を取得する。
    - 次の要素へ移動する。
- `main`メソッド
  - `DataStructure`オブジェクト(`ds`)をインスタンス化する。
  - `printEven`メソッドを呼び出して、偶数インデックス値を持つ配列`arrayOfInts`の要素を出力する。

```java
public class DataStructure {

    // 配列を作成する
    private final static int SIZE = 15;
    private int[] arrayOfInts = new int [SIZE];

    public DataStructure() {
        // 昇順の整数で配列を埋める
        for (int i = 0; i < SIZE; i++) {
            arrayOfInts[i] = i;
        }
    }

    public void printEven() {

        // 配列の偶数インデックス値を出力する
        DataStructureIterator iterator = this.new EvenIterator();
        while (iterator.hasNext()) {
            System.out.print(iterator.next() + "");
        }
        System.out.println();
    }

    interface DataStructureIterator extends java.util.Iterator<Integer> {}

    // インナー クラスはIterator<Integer>インターフェイスを拡張した
    // DataStructureIteratorインターフェイスを実装する

    private class EvenIterator implements DataStructureIterator {

        // 配列の最初から処理を開始する
        private int nextIndex = 0;
    }
}
```