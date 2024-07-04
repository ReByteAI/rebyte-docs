# ファイルローダー

`File Loader` アクションは、以前に imprai にアップロードされたファイルを読み込むことができます。ファイルは imprai の UI または API を介してアップロードされます。

典型的なユースケースは、ユーザーがアップロードしたファイルを処理する必要がある場合です。`File Loader` アクションを使用してファイルを読み込み、そのファイルからデータを抽出できます。

このアクションは、入力として `file_id` を受け取り、そのファイルから抽出されたデータを返します。 `file_id` は imprai にアップロードされたファイルの一意の識別子です。

ファイル形式として。DOC、DOCX、IMG、EPUB、JPEG、JPG、PNG、XLS、XLSX、PPT、PPTX、MD、TXT、RTF、MD、TXT、RTF、RST、PDF、JSON、HTML、EML など様々なデータ型をサポートしています。

## 使い方

- ツールに `File Loader` アクションを追加し、ツールにアップロードするファイルを選択します。

- このファイルの `file_id` を指定し、この一意の `file_id` を必要なときに使用します。

- ツールをアプリに接続すると、ユーザーがファイルをアップロードでき、その `file_id` がツールに渡されます。

- このアクションの出力は、ファイルから抽出されたデータを含む JSON 形式です。

<!-- **Config**

* **File ID:** ファイルの UUID、固定または変数への参照が可能です。

**Output**

* ファイルから抽出された構造化データの JSON 配列
* ファイルの種類に応じて、構造化データは異なります。例えば、PDF ファイルの場合、構造化データはページのリストで、各ページは段落のリストで、各段落は行のリストで、各行は単語のリストです。JSON ファイルの場合、構造化データは JSON オブジェクトそのものです。 -->

<!-- **Example** -->

<!-- * [File Loader](https://imprai.ai/p/21b2295005587a5375d8/agent/bb48d1c1658b5a08917a) -->

<!-- **Error Handing**

* If the file id is invalid, or the file is not supported, the action will return an empty array. -->

<!-- ## サンプルツール

- [ファイルローダー](https://imprai.ai/p/21b2295005587a5375d8/callable/bb48d1c1658b5a08917a/editor) -->
