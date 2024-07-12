# 以前のアクションの出力を参照する方法

アクションの種類に応じて、以前のアクションの出力を参照する方法には 2 つあります。

## プレーン JavaScript 構文

`env.state`オブジェクトを使用して、以前のアクションの出力にアクセスします。例えば、`INPUT`アクションの出力にアクセスする場合、`env.state.INPUT`を使用します。

```javascript
const llmOutput = env.state.LLM_CALL;
```

この構文は、JavaScript をサポートするすべてのフィールドで使用されます。

## プロンプトテンプレート言語

この構文は、プロンプトテンプレート言語をサポートする他のフィールドで使用されます。以前のアクションの出力にアクセスするには、`{{}}`構文を使用します。例えば、`INPUT`アクションの出力にアクセスする場合、`{{INPUT}}`を使用します。

例えば、`INPUT`アクションの最初のメッセージにアクセスする場合、`{{INPUT.messages[0].content}}`を使用します。

```markup
{{INPUT.messages[0].content}}
```

プロンプトテンプレート言語は、LLM モデルのプロンプトを生成するためのテンプレートを作成するためのシンプルな言語です。このプロンプトテンプレート言語は[Jinja](https://jinja.palletsprojects.com/en/3.1.x/)テンプレート言語のサブセットです。以下にプロンプトテンプレート言語の使用例を示します。構文に関する詳細は[Jinja のドキュメント](https://jinja.palletsprojects.com/en/3.1.x/templates/)を参照してください。

\{\{ と \}\} は式に使用されます。

```
{{ 1 + 1 }}
```

変数を参照する場合

```
{{ variable_name }}
```

ステートメントには以下のように使用されます。

```markup
{% raw %}
{% for i in range(10) %}

    {{ i }}

{% endfor %}
{% endraw %}
```

{# と #} はコメントに使用されます。テンプレートの一部をコメントアウトするには、{# #}で囲みます。そのタグの間にあるものはレンダリングされません。

```
{# これはコメントです #}
```

オブジェクトの属性にはドット（.）を使用してアクセスします。例えば、`{{ product.name }}`のように使用します。配列やタプルの特定のメンバーには、ゼロベースのインデックスを使用してアクセスします。ドット（.）の後に変数を使用することはできません。

```
{{ product.name }}
{{ product[0] }}
```

テストは、ある表現が特定の条件を満たすかどうかを確認するために使用され、if ブロックで is キーワードを使って行います。例えば、表現が奇数であるかどうかをテストする場合、以下のように書きます。

```markup
{% raw %}
{% if number is odd %}

    これは奇数です

{% endif %}
{% endraw %}
```

テストは否定することもできます。

```markup
{% raw %}
{% if number is not odd %}

    これは奇数ではありません

{% endif %}
{% endraw %}
```