# ツール API

ツール API を使用すると、独自のアプリケーション内で AI ツールを構築できます。メッセージの送信、ファイルのアップロード、スレッドの作成など、ツールと対話するための一連の API を提供します。

## 概要

ツール API の典型的な統合フローは以下の通りです：

1. `Model`、`Data`、`Tools`、`Control Flow`などのカスタムアクションを定義して imprai ツールエディタでツールを作成します。使用したいモデルとパラメータを選択します。

2. ユーザーが会話を開始するときにスレッドを作成します。

3. ユーザーが質問するたびにスレッドにメッセージを追加します。

4. スレッド上でツールを実行して応答を生成します。

## ステップバイステップ

1. ツールを作成します。

ここでは、["Chat with GPT3.5 agent"](https://imprai.ai/p/21b2295005587a5375d8/callable/f4222f209267e5b24cda/editor)を例として使用します。まずツールをテストし、期待通りに動作することを確認してください。また、「デプロイ」をクリックして API で使用可能にします。

2. スレッドを作成します。

API を使用する前に、サイドバーの API コンソールから API キーを取得してください。このキーを使用してリクエストを認証します。

スレッドを作成する際には、作成時にメッセージをスレッドに追加できます。また、スレッドにメタデータを付与することもできます。これにより、オブジェクトに関する追加情報を構造化形式で保存することができます。

```shell
curl 'https://imprai.ai/api/sdk/threads' \
--H 'Content-Type: application/json' \
--H 'Authorization: Bearer $imprai_KEY' \
--H 'Cookie: NEXT_LOCALE=en' \
--d '{
     "metadata": {
        "user": "abc123"
      },
    "messages":[
        {
            "role":"user",
            "content":"Hi, how are you?"
        },
        {
            "role":"assistant",
            "content":"Hi, I am good. What about you? Is there anything I can help?"
        }
    ]
}'
```

レスポンスにはスレッド ID が含まれています。このスレッド ID を使用して、スレッドにメッセージを追加し、ツールをスレッド上で実行できます。

- レスポンスの例

```shell
{
    "id": "UHSHhnkWGElWShQS5ZtOa",
    "created_at": 1714050659
}
```

3. スレッドにメッセージを追加します。

```shell
curl 'https://imprai.ai/api/sdk/threads/{thread_id}/messages' \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $imprai_KEY" \
  -d '{
      "role": "user",
      "content": "How does AI work? Explain it in simple terms."
    }'
```

レスポンスにはメッセージ情報が含まれています。

- レスポンスの例

```shell
{
    "id": "u8YmkrO4lYZD8r8Nl5cFh",
    "created_at": 1714051597,
    "thread_id": "UHSHhnkWGElWShQS5ZtOa",
    "role": "user",
    "content": "Teach me how to make pancake."
}
```

4. スレッド上でツールを実行します。

ツールをスレッド上で実行するには、ツールをデプロイした際の URL を取得し、この URL にリクエストを送信します。

```shell
curl -L https://imprai.ai/api/sdk/p/21b2295005587a5375d8/a/f4222f209267e5b24cda/r \
    -H "Authorization: Bearer $imprai_KEY" \
    -H "Content-Type: application/json" \
    -d '{
    "version": 1,\
    "config": {
        "MODEL_CALL": {
            "provider_id": "open
```
