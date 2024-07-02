# スレッド

## スレッドの作成

`POST https://rebyte.ai/api/sdk/threads`

新しいスレッドを作成します。

**リクエストボディ**

- messages: スレッドを開始するためのメッセージの配列です。
- metadata: オブジェクトに添付できる 16 組のキーと値のセットです。これにより、オブジェクトに関する追加情報を構造化形式で保存できます。キーは最大 64 文字、値は最大 512 文字です。

**リクエスト例**

```shell
curl 'https://rebyte.ai/api/sdk/threads' \
--H 'Content-Type: application/json' \
--H 'Authorization: Bearer $REBYTE_KEY' \
--H 'Cookie: NEXT_LOCALE=en' \
--data '{
     "metadata": {
        "user": "abc123"
      }
}'
```

**リターン**

スレッドオブジェクト。

**例**

```json
{
  "id": "2hWVPNfrHv1IiVN7ia-4P",
  "created_at": 1710481773,
  "metadata": {
    "user": "abc123"
  }
}
```

### スレッドを一覧表示

`GET https://rebyte.ai/api/sdk/threads`

スレッドの一覧を取得します。

**クエリパラメータ**

- limit: 返されるスレッドの最大数を指定する整数。デフォルトは 20。
- order: スレッドの返却順序を指定する文字列。デフォルトは desc。
- before: ページネーションで使用するカーソルとして使用される文字列。after はリスト内の位置を定義するオブジェクト ID です。
- after: ページネーションで使用するカーソルとして使用される文字列。before はリスト内の位置を定義するオブジェクト ID です。

**リクエストの例**

```shell
curl  'https://rebyte.ai/api/sdk/threads?limit=10&order=desc' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer $REBYTE_KEY' \
-H 'Cookie: NEXT_LOCALE=en'
```

**リターン**

スレッドオブジェクトのリスト。

**例**

```json
{
  "list": [
    {
      "id": "2hWVPNfrHv1IiVN7ia-4P",
      "created_at": 1710481773,
      "metadata": {
        "user": "abc123"
      }
    },
    {
      "id": "NGXTNrg-34seXYc-PCVFu",
      "created_at": 1710415453,
      "metadata": {
        "user": "abc123"
      }
    },
    {
      "id": "MRlX-SOAo5gAx1mxBe7S4",
      "created_at": 1710407916
    }
  ]
}
```

### スレッドの取得

`GET https://rebyte.ai/api/sdk/threads/{thread_id}`

ID でスレッドを取得します。

**パスパラメータ**

- thread_id (必須): 取得するスレッドの ID を含む文字列。

**リクエスト例**

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer $REBYTE_KEY' \
-H 'Cookie: NEXT_LOCALE=en'
```

**リターン**
指定された ID に一致するスレッドオブジェクト。

**例**

```json
{
  "id": "cB1-_3wh5ZWtUPJU4xIuU",
  "created_at": 1710415223,
  "metadata": {
    "user": "czy",
    "modified": "true"
  }
}
```

### スレッドの更新

`POST https://rebyte.ai/api/sdk/threads/{thread_id}`

スレッドを更新します。

**パスパラメータ**

- thread_id (必須): 更新するスレッドの ID を含む文字列。

**リクエストボディ**

- metadata: オブジェクトに添付できる 16 組のキーと値のセット。これにより、オブジェクトに関する追加情報を構造化形式で保存できます。キーは最大 64 文字、値は最大 512 文字です。

**リクエスト例**

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer $REBYTE_KEY' \
-H 'Cookie: NEXT_LOCALE=en' \
--data ' {
    "metadata":
    {
        "modified": "true",
        "user": "czy"
    }
 }'
```

**リターン**
指定された ID に一致する変更されたスレッドオブジェクト。

**例**

```json
{
  "id": "cB1-_3wh5ZWtUPJU4xIuU",
  "created_at": 1710415223,
  "metadata": {
    "modified": "true",
    "user": "czy"
  }
}
```
