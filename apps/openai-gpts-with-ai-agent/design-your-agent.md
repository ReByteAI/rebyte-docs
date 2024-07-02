- 自動生成されたテンプレートには、すでにいくつかのアクションが作成されています。
- 異なるアクションの間にあるプラスボタンを使用して、「Knowledge Search」アクションを追加します。

<figure><img src="../../images/deign-your-agent-1.png"></figure>

- 先ほど作成したナレッジベースを選択し、結果の数を設定します。このアクションにより、指定されたナレッジベースで検索を実行し、結果を返すことができます。
- チャンク内で検索結果をすべて確認できます。

<figure><img src="../../images/deign-your-agent-2.png"></figure>

- より良い使用のために、このエージェントには3つの「コード」アクションがあります。
    - 最初のものは、最新メッセージから内容を抽出するものです。
        
        <figure><img src="../../images/deign-your-agent-3.png"></figure>
        
    - 2つ目の「コード」アクションは、「Knowledge Search」アクションの結果を連結するものです。
        
        <figure><img src="../../images/deign-your-agent-4.png"></figure>
        
    - もう1つの「Generate Answer」と呼ばれる「コード」アクションを使用して、検索結果と応答を連結します。
        
        <figure><img src="../../images/deign-your-agent-5.png"></figure>
        
- 次に、「Language Model Chat Interface」アクションを使用して、検索結果に基づいて応答を取得します。
- エディターでモデルに指示を書くことで、モデルに何をしてほしいかを記述します。モデルが応答を生成してくれます。

<figure><img src="../../images/deign-your-agent-6.png"></figure>