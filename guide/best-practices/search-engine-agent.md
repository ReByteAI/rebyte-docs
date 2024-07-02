# 検索エージェント

ウェブページの内容を要約します。

### `Datasets`でテストデータを設定

```json
[
  {
    "role": "user",
    "content": "Who won the last UEFA Champions League?"
  },
  {
    "role": "assitant",
    "content": "The last winner of the UEFA Champions League was Manchester City in the 2022-23 season. This was their first title in the competition. Real Madrid holds the record for the most victories in the Champions League, having won it 14 times [0][1]."
  },
  {
    "role": "user",
    "content": "Who scored the winning goal?"
  }
]
```

### `Code Action`を使用して最後のメッセージを取得

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
  return env.state.INPUT.messages.slice(-1)[0].content;
}
```

### `Code Action`を使用してチャット履歴を取得

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
  return env.state.INPUT.messages.slice(0, env.state.INPUT.messages.length - 1).map((m) => m.content).join("\n");
}
```

### `Code Action`を使用してコンテンツを抽出

```txt
{# あなたのプロンプトをここに入力してください。例: '以下の内容に基づいてこれらの質問に答えてください。' #}
{# プロンプトの開始: #}
これが質問です: {{EXTRACT_QUESTION}}
これが会話履歴です: {{HISTORY}}

会話履歴を参考にして質問に必要な文脈を追加してください。文脈が関連しない場合は、質問を変更しないでください。ここで質問を与えてください:
```

### `Google_search`を使用して関連コンテンツを検索
```javascript
{{REFINED_QUESTION.completion.text}}
```

### `Code Action`を使用してコンテンツを抽出

```javascript
// Google検索のオーガニック結果からタイトル、スニペット、リンクを抽出します。
// 3つに制限
_fun = (env) => {
  if (!env.state.GOOGLE_SEARCH.organic_results) {
    return [
      {
        title: "",
        link: ""
      }
    ]
  }

  return env.state.GOOGLE_SEARCH.organic_results.map((r) => {
    return { title: r.title, link: r.link, snippet: r.snippet };
  }).slice(0, 3);
}
```

### 結果を並列処理のためにマッピング

```javascript
SEARCH_EXTRACT
```

### `WEB_CRAWL`を使用してページをスキャン
```javascript
{{SEARCH_RESULT_LOOP.link}}
```

### `Code Action`を使用してコンテンツを抽出
```javascript
// 各リンクについて、そのコンテンツをクロールし、2000バイトに制限
_fun = (env) => {
  return {
    content: env.state.WEB_CRAWL_1.data ? env.state.WEB_CRAWL_1.data[0].results[0].text.slice(0, 2000) : "",
  };
}
```

### LLMを使用してコンテンツを分析
```json
{# あなたのプロンプトをここに入力してください。例: '以下の内容に基づいてこれらの質問に答えてください。' #}
{# プロンプトの開始: #}

次の質問に基づいて:
"""
{{EXTRACT_QUESTION}}
"""

以下のコンテンツから質問に関連するテキストを抽出し、要約してください:
"""
{# {{GOOGLE_REFERENCES.content}} #}
{{SEARCH_RESULT_LOOP.snippet}}
"""

抽出された要約コンテンツ:
"""
```

### `Code Action`を使用してコンテンツを抽出
```javascript
_fun = (env) => {
  return {
    summary: env.state.MODEL_SUMMARIZE.completion.text.trim(),
    link: env.state.SEARCH_RESULT_LOOP.link
  };
}
```

### `Code Action`を使用してコンテンツを抽出およびプロンプトを作成（続き）

```javascript
const _example = (example) => {
  let prompt = "CONTENT:\n";
  prompt += '"""\n';
  example.forEach((d, i) => {
    if (i > 0) {
      prompt += '\n';
    }
    prompt += `link [${i}]: ${d.link}\n`;
    prompt += `content: ${d.summary.replaceAll('\n', ' ')}\n`;
  });
  prompt += '"""\n';
  console.log(prompt);
  return prompt;
}

_fun = (env) => {
  let prompt = 'Given the following questions, reference links and associated content, create a final answer with references. If some of answer can be formatted in table format, format in table format. Answer should be accurate and concise. \n\n Never tell me "As a language model ..." or "As an artificial intelligence...", I already know you are a LLM. Just tell me the answer. \n\n';
  prompt += "QUESTION:" + env.state.EXTRACT_QUESTION + "\n";
  prompt += _example(env.state.FORMAT_SUMMARY);

  prompt += `FINAL:\n"""\n`;

  return { prompt };
}
```

### プロンプトをLLMに送信
```json
{{FINAL_PROMPT.prompt}}
```

### `OUTPUT_STREAM`を出力として抽出
```json
{{FINAL_PROMPT.prompt}}
```

## まとめ

以上の手順で、ウェブページの内容を要約する検索エージェントを作成することができます。このエージェントは、ユーザーの質問を受け取り、関連するウェブコンテンツを検索して要約し、質問に対する答えを提供します。

主要なステップは次の通りです：

1. **テストデータの設定：** `Datasets` にテストデータを設定します。
2. **最後のメッセージの取得：** `Code Action` を使用して最後のメッセージを取得します。
3. **チャット履歴の取得：** `Code Action` を使用してチャット履歴を取得します。
4. **コンテンツの抽出：** `Code Action` を使用して質問と履歴からコンテンツを抽出します。
5. **Google検索を使用して関連コンテンツを検索：** `Google_search` を使用して関連コンテンツを検索します。
6. **検索結果の抽出：** `Code Action` を使用して検索結果を抽出します。
7. **ページのスキャン：** `WEB_CRAWL` を使用してページをスキャンします。
8. **コンテンツの分析と要約：** LLMを使用してコンテンツを分析し、要約します。
9. **プロンプトの作成と送信：** `Code Action`を使用してプロンプトを作成し、LLMに送信します。
10. **最終結果の出力：** `OUTPUT_STREAM`を使用して最終結果を出力します。

これらのステップを通じて、ユーザーの質問に対して迅速かつ正確に答える検索エージェントを実装することができます。