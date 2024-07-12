# ツール作成の例

ツール作成は「デザイン」画面で行います。以下がその画像です：

<figure><img src="../images/screenshot-20240703-123724.png" alt=""></figure>

このツールは`INPUT`、`EXTRACT_QUESTION`、`MESSAGES`、`RETRIEVALS`、`RETRIEVALS＿RESULT`、`OUTPUT_STREAM`、`GET_ANSWER`、`OUTPUT`の８つのブロックから構成されています。

- `INPUT`はツールを作成する上で必須で、ここではユーザーの質問を JSON 形式に変換するブロックです。

<figure><img src="../images/screenshot-20240703-124735.png" alt=""></figure>

- `EXTRACT_QUESTION`はアクションの 1 つである`Code`を使用して`INPUT`の content を取得するブロックです。

<figure><img src="../images/screenshot-20240703-125745.png" alt=""></figure>

- `MESSAGES`はアクションの 1 つである`Code`を使用して`INPUT`の messages をマッピングして role と content を返すブロックです。

<figure><img src="../images/screenshot-20240703-130207.png" alt=""></figure>

- `RETRIEVALS`はアクションの 1 つである`Knowledge Serach`を使用してナレッジデータベース検索するブロックです。ここではクエリとして`EXTRACT_QUESTION`を使用しています。

<figure><img src="../images/screenshot-20240703-131027.png" alt=""></figure>

ここの部分ではメタデータが付与されるので、そのメタデータをダウンストリームアクションで使用できます。

<figure><img src="../images/screenshot-20240703-131221.png" alt=""></figure>

- `RETRIEVALS＿RESULT`はアクションの 1 つである`Code`を使用して`RETRIEVALS`の document_id と chunk.text を取得し整形して返すブロックです。document_id を使用することで参照元を表示させることできます。

<figure><img src="../images/screenshot-20240703-131854.png" alt=""></figure>

<figure><img src="../images/screenshot-20240703-131945.png" alt=""></figure>

- `OUTPUT_STREAM`はアクションの 1 つである`Language Model Chat Interface`を使用しています。ここでは`RETRIEVALS＿RESULT`の情報に基づいて model に指示(プロンプト)をだし、そのプロンプトを system の content として，回答を assistant の content として`INPUT`に追加するブロックです。

<figure><img src="../images/screenshot-20240703-132441.png" alt=""></figure>

<figure><img src="../images/screenshot-20240703-132506.png" alt=""></figure>

- `GET_ANSWER`はアクションの 1 つである`Code`を使用して`OUTPUT_STREAM`の role の assistant とその content を返すブロックです。

<figure><img src="../images/screenshot-20240703-133850.png" alt=""></figure>

- `OUTPUT`は必須で、ここで`GET_ANSWER`の内容を受け取ります。

<figure><img src="../images/screenshot-20240703-134010.png" alt=""></figure>

最終的に`OUTPUT`の content がユーザーへの回答になります。
