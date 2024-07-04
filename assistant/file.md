# ファイル

## ファイルのアップロード

`POST https://imprai.ai/api/sdk/files`

さまざまなエンドポイントで使用できるファイルをアップロードします。

**リクエストボディ**

- file (必須): アップロードするファイルオブジェクト。

**リクエスト例**

```shell
curl 'https://imprai.ai/api/sdk/files' \
  -H "Authorization: Bearer $imprai_KEY" \
  -F file="@mydata.jsonl"
```

**リターン**

メッセージ、fileId、パスを含むオブジェクトを返します。

**レスポンス**

```json
{
  "message": "upload file success",
  "fileId": "09343664-****-****-a4e5-02aa25d15b54",
  "path": "1b242a2dea62c6******/09343664-****-4d43-a4e5-02aa25d15b54"
}
```

## ファイルの一覧取得

`GET https://imprai.ai/api/sdk/files`

ファイルのリストを取得します。

**リクエスト例**

```shell
curl 'https://imprai.ai/api/sdk/files' \
  -H "Authorization: Bearer $imprai_KEY"
```

**リターン**

ファイルのリストを返します。

**レスポンス**

```json
{
  "files": [
    {
      "uuid": "d723538c-d188-4c24-80f6-71b27b43a76e",
      "name": "api_data.json",
      "mimeType": "application/json",
      "size": 18119,
      "projectId": 160,
      "createdAt": "2024-03-14T11:26:15.240Z"
    },
    {
      "uuid": "2b3dc1e9-634d-4bd5-b9d7-94a9b4a0662c",
      "name": "每日推特.txt",
      "mimeType": "text/plain",
      "size": 1589,
      "projectId": 160,
      "createdAt": "2023-12-28T07:17:24.733Z"
    }
  ]
}
```

## ファイルの取得

`GET https://imprai.ai/api/sdk/files/{fileId}`

fileId でファイルを取得します。

**リクエスト例**

```shell
curl 'https://imprai.ai/api/sdk/files/{fileId}' \
  -H "Authorization: Bearer $imprai_KEY" \
```

**リターン**

ファイルオブジェクトを返します。

**レスポンス**

```json
{
  "file": {
    "name": "api_data.json",
    "uuid": "ac1722a6-76cb-45d3-bcfe-7117939e0f52",
    "projectId": 160,
    "createdAt": "2024-03-14T11:15:56.257Z",
    "mimeType": "application/json",
    "size": 18119
  }
}
```

## ファイルコンテンツの取得

`GET https://imprai.ai/api/sdk/files/{fileId}/content`

fileId でファイルコンテンツを取得します。

**リクエスト例**

```shell
curl 'https://imprai.ai/api/sdk/files/{fileId}/content' \
  -H "Authorization: Bearer $imprai_KEY" \
```

**リターン**

ファイルのコンテンツを返します。

**レスポンス**

```json
ファイルのコンテンツ...
```

## ファイルの削除

`DELETE https://imprai.ai/api/sdk/files/{fileId}`

fileId でファイルを削除します。

**リクエスト例**

```shell
curl --location --request DELETE 'https://imprai.ai/api/sdk/files/{file_id}' \
--H 'Authorization: Bearer $imprai_KEY'
```

**リターン**

メッセージオブジェクトを返します。

**レスポンス**

```json
{
  "message": "deleted",
  "fileId": "09343664-ddb2-4d43-a4e5-02aa25d15b54"
}
```
