# メッセージ

## メッセージの挿入

`POST https://rebyte.ai/api/sdk/threads/{threadId}/messages`

スレッドに新しいメッセージを作成します。

**パスパラメータ**

- thread_id (必須): メッセージを作成するスレッドの ID を含む文字列。

**リクエストボディ**

- role (必須): メッセージを作成するエンティティの役割を含む文字列。現在は user のみがサポートされています。
- content (必須): メッセージの内容を含む文字列。
- file_ids: メッセージで使用するファイルの ID のリスト。メッセージに最大 10 個のファイルを添付できます。ファイルにアクセスして使用するための retrieval や code_interpreter などのツールで便利です。
- metadata: オブジェクトに添付できる 16 組のキーと値のセット。これにより、オブジェクトに関する追加情報を構造化形式で保存できます。キーは最大 64 文字、値は最大 512 文字です。

**リクエスト例**

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages' \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
  -d '{
      "role": "user",
      "content": "How does AI work? Explain it in simple terms."
    }'
```

**リターン**

メッセージオブジェクト。

**例**

```json
{
  "id": "W_DPv1bwUQ50PC52f44Uo",
  "created_at": 1710415825,
  "thread_id": "p_DFiNmczwUWZjcl47U9X",
  "role": "user",
  "content": "How does AI work? Explain it in simple terms.",
  "metadata": {
    "user": "czy1"
  }
}
```

## メッセージの一覧表示

`GET https://rebyte.ai/api/sdk/threads/{threadId}/messages`

スレッド内のメッセージの一覧を取得します。

**パスパラメータ**

- thread_id (必須): メッセージを作成するスレッドの ID を含む文字列。

**クエリパラメータ**

- limit: 整数、デフォルトは 20。返されるオブジェクトの数の制限。制限は 1 から 100 の範囲内であり、デフォルトは 20 です。

- order: 文字列、デフォルトは desc。オブジェクトの created_at タイムスタンプでのソート順序。昇順は asc、降順は desc です。

- after: 文字列、ページネーションに使用するカーソル。after はリスト内の位置を定義するオブジェクト ID です。例えば、リストリクエストを行い、obj_foo で終わる 100 オブジェクトを受け取った場合、次の呼び出しで after=obj_foo を含めると、次のページのリストを取得できます。

- before: 文字列、ページネーションに使用するカーソル。before はリスト内の位置を定義するオブジェクト ID です。例えば、リストリクエストを行い、obj_foo で終わる 100 オブジェクトを受け取った場合、次の呼び出しで before=obj_foo を含めると、前のページのリストを取得できます。

**リクエストの例**

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages'     \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
```

**リターン**

メッセージのリストを返します。

**例**

```json
{
  "list": [
    {
      "id": "W_DPv1bwUQ50PC52f44Uo",
      "created_at": 1710415825,
      "thread_id": "p_DFiNmczwUWZjcl47U9X",
      "role": "user",
      "content": "How does AI work? Explain it in simple terms.",
      "metadata": {
        "user": "czy4"
      }
    }
  ]
}
```

## メッセージの取得

`GET https://rebyte.ai/api/sdk/threads/{threadId}/messages
