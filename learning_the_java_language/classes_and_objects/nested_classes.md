# Nested Classes（入れ子クラス）

クラスの中にクラスを定義したものを _nested class（ネスティッド クラス、入れ子クラス）_ と呼ぶ。

例

```java
class OuterClass {
  //...
  class NestedClass {
    //...
  }
}
```

---

- 用語（入れ子クラスの分類）
  - static: _static nested class(スタティック ネスティッド クラス、静的入れ子クラス)_
  - staticでない: _inner class（インナー クラス、内部クラス）_

---

入れ子クラスは、それを囲むクラス（アウター クラス）のメンバー。入れ子クラスは他のメンバー（`private`を含む）へアクセスできる。上記の例における `OuterClass` のメンバーとして、入れ子クラスは `private`・`public`・`protected`・パッケージ プライベート のいずれとしても定義できる。（アウター クラス は、`public` か パッケージ プライベート のいずれかで定義できる。）

## Why Use Nested Classes?(入れ子クラスを使う理由)

- **1ヶ所でのみ使われるクラスを論理的にグループ化する方法であるため。** あるクラスAが、クラスBからのみ使われるとする。また、クラスAをクラスBへ埋め込むのが論理的に妥当だとする。クラスAのような「ヘルパー クラス」を入れ子にすることにより、パッケージが効率的になる。

- **カプセル化を高める。** クラスA、Bがあるとする。クラスBがクラスAのプライベート メンバーへアクセスしたいとする。クラスBをクラスAの入れ子クラスにする。そうすると、クラスAのメンバーはプライベートのままでよくなる。また、クラスBを他のクラスから隠蔽できる。

- **可読性と保守性が向上する。** 小さいクラスをトップレベル（入れ子ではない） クラスへ入れ子にすることにより、関連するコードを近くへ配置することになる。

## Static Nested Class(静的入れ子クラス)

クラス メソッドや変数と同様に、静的入れ子クラスもアウター クラスと紐付いている。静的クラス メソッドと同様に、静的入れ子クラスもアウター クラス のインスタンス メソッドや変数へ直接アクセスできない: オブジェクトの参照を通じてのみアクセスできる。

---

**ノート:** 静的入れ子クラスは、他のトップレベルのクラスと同様、アウター クラス（や他のクラス）のインスタンス メンバーと連携する。つまり、静的入れ子クラスはパッケージングの都合で他のクラスに入れ子にされているが、振る舞いの上ではトップレベルのクラスである。

---

静的入れ子クラスへアクセスする時は、アウタークラス名を前に付加する。

```java
OuterClass.StaticNestedClass nestedObject = new OuterClass.StaticNestedClass();
```

## Inner Clases(インナー クラス）

インスタンスのメソッドや変数と同様、インナー クラスはアウター クラスのインスタンスと紐付いている。また、オブジェクトのメソッドやフィールドへ直接アクセスできる。staticなメンバーを定義できない。

インナー クラスをインスタンス化するには、最初にアウター クラスを定義しなければならない。それからアウター クラスの中でインナー オブジェクトを生成する。

```java
OuterClass outerObject = new OuterClass();
OuterClass.InnerClass innerObject = outerObject.new InnerClass();
```

### インナー クラスの2つの特別な種類

- [ローカル クラス](./local_classes.md)
- [匿名クラス](./anonymous_classes.md)

## Shadowing(シャドゥイング)

特定のスコープ（インナー クラスやメソッド定義）で、型の定義（メンバー変数やパラメーター名）がアウター クラスの別の定義と同じ名前の場合、インナー クラスの定義がアウター クラスの定義を隠してしまう。隠れてしまった定義を名前だけで参照できない。

```java
public class ShadowTest {
    public int x = 0;

    class FirstLevel {
        public int x = 1;

        void methodInFirstLevel(int x) {
            System.out.println("x = " + x); // 23
            System.out.println("this.x = " + this.x); // 1
            System.out.println("ShadowTest.this.x = " + ShadowTest.this.x); // 0
        }
    }

    public static void main(String... args) {
        ShadowTest st = new ShadowTest();
        ShadowTest.FirstLevel fl = st.new FirstLevel();
        fl.methodInFirstLevel(23);
    }
}
```

## Serialization(シリアル化)

[ローカル クラス](./local_classes.md) や [匿名クラス](./anonymous_classes.md) を含むインナー クラスの[シリアル化](../../jndi/objects/serial.md)は極めて非推奨とされている。Javaコンパイラーがインナー クラスのようなある構成物をコンパイルする時、_合成構成物(synthetic constructs)_ が生成される。ソース コードとは対応しないクラス、メソッド、フィールドや他の構成物がある。合成構成物により、JVMを変えることなく新しいJavaの言語機能をJavaコンパイラーが実装できる。しかし、合成構成物はJavaコンパイラーの実装によって異なる。つまり、`.class`ファイルが異なる可能性がある。その結果、インナー クラスをシリアル化し、異なるJREの実装でデシリアル化する場合に、互換性の問題が発生するかもしれない。インナー クラスがコンパイルされた時に生成される合成構成物に関する詳細は、「[メソッド パラメーターの名前を取得する](../../reflect/member/methodparameterreflection.md)」の「[暗黙と合成パラメーター](../../reflect/member/methodparameterreflection.md#implcit_and_synthetic)」のセクションを参照のこと。