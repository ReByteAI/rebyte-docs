# 投資家タイプクイズアプリの構築

この包括的なガイドでは、imprai のツールと Typeform API を使用して投資家タイプクイズアプリを作成する手順を説明します。Typeform の API はユーザーフレンドリーなフォームやアンケートを作成できるため、ユーザーとの明確で効果的なエンゲージメントに最適です。

最終的なアプリの結果は次の通りです：

![app](https://res.cloudinary.com/dfjwtidnh/image/upload/v1710077600/investor-0_uqamir.png)

## 前提条件

- [Typeform アカウント](https://www.typeform.com/)と、[Typeform API ドキュメント](https://www.typeform.com/developers/)の十分な理解。
- imprai のエージェントとアプリに関する基本的な知識、およびいくつかのプログラミング知識。

## ビルド方法

アプリはシンプルなロジックで動作します。まずユーザーから基本情報を収集し、その後 Typeform API を使用して詳細な質問を行うフォームを生成します。ユーザーがフォームに入力して送信すると、その回答が分析され、投資家タイプが決定されます。

### 手順

1. **ユーザーの入力から情報を収集する:**

   imprai の`model-chat`アクションを利用して、ユーザーの初期入力に基づいて情報を抽出します。

   ![gather info](https://res.cloudinary.com/dfjwtidnh/image/upload/v1710077600/intestor-1_vj3kej.png)

2. **Typeform API を使用してフォームを作成する:**

   事前に書かれたコードを実装して、フォームの適切な質問を選択します。その後、アクションを通じて Typeform API を呼び出し、フォームの URL を生成します。

![code](https://res.cloudinary.com/dfjwtidnh/image/upload/v1710077600/investor-2_sun44v.png)

3. **ユーザーの回答を収集する:**

   ユーザーがフォームを完了して送信すると、「http」アクションを通じて結果を取得します。

![get results](https://res.cloudinary.com/dfjwtidnh/image/upload/v1710077600/investor-3_k9ejp9.png)

4. **ユーザーの入力を分析する:**

   次のモデルチャットアクションを使用して、ユーザーの回答を処理し、投資家タイプを特定します。

   ![analyze](https://res.cloudinary.com/dfjwtidnh/image/upload/v1710077600/investor-4_puom38.png)

### 結論

このプロジェクトは、Typeform などの API を imprai の技術と統合して、インタラクティブでユーザーフォーカスのアプリケーションを作成する力を示しています。投資家タイプクイズアプリは、動的な方法でユーザーを引きつけるだけでなく、彼らの投資嗜好に関する貴重な洞察を提供し、情報に基づいた意思決定を支援します。このガイドで説明された手順は、さまざまなアプリケーションに適用できるフレームワークを提供し、アプリ開発の分野におけるこれらのツールの柔軟性と可能性を示しています。

## デモ

アプリとエージェントの動作を確認するには、以下のリンクを参照してください：

[投資家タイプクイズエージェント](https://imprai.ai/p/21b2295005587a5375d8/callable/ffdc7bd0d262b62cbd03/editor)

[投資家タイプクイズアプリ](https://imprai.ai/copilot/0167ad764f8be5e1bd41/session/6afc350466)
