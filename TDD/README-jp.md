[戻る](../README-jp.md#TDD)

[한국어로 보기](./README.md)

# TDD?

Test-Driven Development (テスト駆動開発)

短い周期の繰り返しに頼るソフトウエア開発プロセス

テストが全体開発を主導する

プログラマーは要求事項の自動化テストケースを作って、

そのテストケースを通るコードを作った後リファクタリングをする過程

# 順序の逆転

- 一般的SW開発

    ロジックに当たる部分のコーディングを終わらせ、そのコードの検証をするためのテストケース作成

- TDD

    要求事項に従うプログラムが備わる機能に対するテストを先に作る

    ⇒ そして、このテストケースを通るためのロジックを作ることに順序を逆転

e.g., 入力した二つの整数の和を出力するプログラム

1. 簡単な目標を設定する

    → 順に三と五を入力されたら、八を出力しなければならない。

2. テストケース設計

    → 三と五を入力すると、(まだ居ないコードを使って)八が出るテストプログラム

3. 相当するテストケースを通るコード作成

    → 二つのinput整数を確認した後、その和をreturnするコード

    ```jsx
    // python3
    // 二つ整数が一つの空白文字と一緒に一行分で取得
    // Ex) >> a b
    x, y = map(int, input().split())
    return x + y
    ```

4. このコードを使ってテストプログラム実行

    → 三と五を入力されると、上のコードで八が出力しなければならない

5. テスト結果が
- 成功の場合、新しテストを追加しながら、相当するテストに通るようにコードをリファクタリング

- 失敗の場合、テストを通るまでコードを修正

# メリット

- プログラマーは実現しようとする機能の要求事項にまともに集中できる

    TDDの順序に合わせてテストを先に作成する

    → 開発者はテスト作成のため、機能の要求事項と明細を事前で完璧に理解しなければならない

    ⇒ ユーザーケースやストーリーを参考して、要求事項分析過程を通じて実現目標をはっきりする

- 新し機能を追加するたび、新し分と既存の機能が同時にうまく動くのか確認可能

    新し機能を追加すると既存機能がちゃんと動かない可能性がある

    → これを防ぐために別機能に対するテストケースを作り、機能が追加されるたびに相当するテストケースを追加する

    ⇒ 機能が追加するたびに全体テストを実行し様々な機能を確認できる

- リファクタリングに役に立つ

    コードが多くなると、可読性とcoding conventionや拡張性とビジネスロジックの改善をためリファクタリングする

    → TDDで開発すると、テストコードでリファクタリングの測定ができる

    (リファクタリング作業で、間欠的にテストを実行し機能を点検)

    ⇒ リファクタリング 作業速度が速くなる

    → その分、クオリティー改善できる
    (クオリティー： オブジェクト指向的か、拡張し安いなのか、 デバッギング時間減少とか)

- 機能点検とテスト文書作成に役に立つ

    テストはコード作成後、機能点検をするため必要なテスト内容の記録を取る文書作成を要求する

    → TDDはこの二つの仕事を自然にできる

    ⇒ その上、コード開発にも役に立つ(要求事項集中、新機能点検、リファクタリング)

# デメリット

- 全体的開発時間が増える

    機能毎にテストケースを作り、ロジックも作ることで仕事が増えるせいだ

    特に、短期成果に集中する企業の立場では困る

- 集中するところを勘違いする可能性がある

    ある機能に対して、色んなテストケースと例外処理テストケースが多くなるかもしれない

    それに、テストコードとロジックコードの優先順位が変わるかもしれない

    → テストコードのためロジックコードの仕組みを変える場合が起きる

- 難しい

    一般的にコーディングした習慣ややり方の切り替えが必要なせいだ

    特に、一般的方法ですでに慣れた経験者ほど切り替える難い(Unlearningを要求する)

    (逆に開発経験が少ないとTDDが安いと。。)

- 進入が難しい

    機能のどの部分をどうやってテストするか設定する方法から、

    開発中のサービスに相当するテストフレームワークの選定まである程度事前学習が必要する

    特に、開発はチーム単位で進むから、TDD適用をためチーム全体がTDDを理解する必要がある

- 偏見と一般化

    決められたツール(単位テストフレームワーク)に頼りすぎることになる

    決められたルールややり方に縛られて、agileじゃ無くなってTDD実現が難しくなる