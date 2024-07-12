# Notion とチャット

ここでは、Notion ページを GPT のナレッジベースとして使用する方法を紹介します。

## ステップ 1：Notion でナレッジを作成する

- ナレッジページに移動し、新しいナレッジを作成します。

<figure><img src="../../images/%25E6%2588%25AA%25E5%25B1%258F2024-01-11_16.58.50.png"></figure>

- ナレッジの名前と説明を入力します。

<figure><img src="../../images/%25E6%2588%25AA%25E5%25B1%258F2024-01-11_16.58.50.png"></figure>

- Notion をナレッジベースとして使用するので、`Notion`をナレッジソースとして選択します。

<figure><img src="../../images/%25E6%2588%25AA%25E5%25B1%258F2024-01-11_17.00.17.png"></figure>

- チャンクサイズを選択し、ナレッジを作成します。

- Notion アカウントを imprai に接続し、使用したいページを選択します。

<figure><img src="../../images/%25E6%2588%25AA%25E5%25B1%258F2024-01-11_17.01.41.png"></figure>

<figure><img src="../../images/%25E6%2588%25AA%25E5%25B1%258F2024-01-11_17.01.41%201.png"></figure>

- これで、Notion のコンテンツがナレッジとして利用できるようになります。

<figure><img src="../../images/%25E6%2588%25AA%25E5%25B1%258F2024-01-11_17.04.55.png"></figure>

## ステップ 2：エージェントをクローンする

- コミュニティで「GPT Builder Actions」タブを選択し、「knowledge_search_agent_for_gpts」をクリックします。

<figure><img src="../../images/Untitled.png"></figure>

- それを自分のプロジェクトにコピーします。

<figure><img src="../../images/Untitled%201.png"></figure>

## ステップ 3：ナレッジを選択し、**デプロイする**

- RETRIEVALS というアクションを見つけ、作成したナレッジを選択します。

<figure><img src="../../images/Untitled%202.png"></figure>

- テストケースを実行し、デプロイします。

このエージェントの設計方法については、[こちら](https://rebyte-ai.gitbook.io/rbyte/apps/openai-gpts-with-ai-agent/design-your-agent)をご覧ください。

## ステップ 4：imprai API で GPT を作成する

- GPT の名前、説明、アバターを入力します。

<figure><img src="../../images/Untitled%203.png"></figure>

- 対応するバージョンの imprai エージェントの OpenAPI コードを GPT のアクションにコピーし、**認証**を API キーとして設定します。

<figure><img src="../../images/Untitled%204.png"></figure>

<figure><img src="../../images/Untitled%205.png"></figure>

- imprai の API キーを入力します（**Auth Type として Bearer を選択**）。

<figure><img src="../../images/Untitled%206.png"></figure>

- 保存して GPT をリリースします！
- これで使用可能です！

<figure><img src="../../images/Untitled%207.png"></figure>

<figure><img src="../../images/Untitled%208.png"></figure>
