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

入れ子クラスは、それを囲むクラス（アウター クラス）のメンバー。内部クラスは他のメンバーへアクセスできる。`private` で定義されいるメンバーへもアクセスできる。上記の例における `OuterClass` のメンバーとして、入れ子クラスは `private`・`public`・`protected`・パッケージ プライベート のいずれとしても定義できる。（アウター クラス は、`public` か パッケージ プライベート のいずれかで定義できる。）