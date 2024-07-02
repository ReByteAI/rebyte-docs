# ウェブページ要約エージェント

ウェブページの内容を要約します。

### `Datasets`でテストデータを設定

```json
[
  {
    "role": "user",
    "content": "https://book.douban.com/subject/30360449/"
  }
]
[
  {
    "role": "user",
    "content": "Introduce this web page: https://towardsdatascience.com/an-introduction-to-openai-function-calling-e47e7cd7680e"
  }
]
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // 前のアクションの出力を参照するために `env.state.Action_NAME` を使用します。
  return env.state.INPUT.messages.slice(-1)[0].content;
}
```

### LLMを使用してユーザーの入力を処理

```javascript
You're a link extractor, which extracts http or https links from given text, output the result as a json format, output contains two fields, first is link, which contains the link extracted from text, second is language, which contains language code of given question.
Here's the given text, let's begin:
{{EXTRACT_QUESTION}}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // 前のアクションの出力を参照するために `env.state.Action_NAME` を使用します。
  const output = JSON.parse(env.state.REFINE.completion.text);
  // linkが存在する場合、そのlinkを出力
  // linksが存在する場合、最初の要素を出力
  return {
    link: output.link ? output.link : (output.links ? output.links[0] : ""),
    language: output.language ?? 'en'
  };
}
```

### `WEB_CRAWL Action`を使用して情報を収集

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  let content = env.state.WEB_CRAWL_1.data ? env.state.WEB_CRAWL_1.data[0].results[0].text.slice(0, 3000) : "";
  content = content.replace(/\n/g, ""); // 改行を削除
  return {
    content: content,
  };
}
```

### ウェブページの内容をLLMに送信

```javascript
Your role is that of a text editor. 
You are expected to peruse the texts provided to you, comprehending them fully, and then distill and summarize them for me. The summary should encapsulate the main theme and essential details of the original text. It should be succinct and expressed in your own words. 
The contents that need to be summarized will be enclosed within three single quotation marks.
 
The summary should be conducted in accordance with the following regulations:
1. Thematic Statement: Succinctly summarize the main theme or key point of the original text. 
2. Key Details: Enumerate the crucial details or facts from the original text that support the main theme or point. 
3. Overall Conclusion: Distill the conclusion of the original text or the position of the author.
 
Please organize the summary according to the following structure and reply me:
Introduction: Introduce the main theme or background of the original text.(New line)
Body Paragraph: List and explain the key details and arguments from the original text, summarizing them in your own words. (New line)
Conclusion: Summarize the main points of the original text or present the author's conclusion.(New line)
 
This is the content that requires summarization:

please reply to me with the phrase: "I apologize for being unable to retrieve content from the URL you provided. Please verify the correctness of the web address"
 
{{CODE_1.content}}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // 前のアクションの出力を参照するために `env.state.Action_NAME` を使用します。
  return {
    role: "assistant",
    content: env.state.OUTPUT_STREAM.completion.text,
    retrievals: env.state.RETRIEVALS
  };
}
```

### 最終結果の出力

```javascript
// 最終結果を出力するためのコード片
_fun = (env) => {
  return {
    role: "assistant",
    content: env.state.FINAL_OUTPUT.content,
    retrievals: env.state.FINAL_OUTPUT.retrievals
  };
}
```

## まとめ

以上の手順を通じて、ウェブページの内容を要約するエージェントを作成することができます。このエージェントは、ユーザーから
# Webページ要約エージェント

Webページの内容を要約します。

### `Datasets`でテストデータを設定

```json
[
  {
    "role": "user",
    "content": "https://book.douban.com/subject/30360449/"
  }
]
[
  {
    "role": "user",
    "content": "Introduce this web page: https://towardsdatascience.com/an-introduction-to-openai-function-calling-e47e7cd7680e"
  }
]
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // 前のアクションの出力を参照するために `env.state.Action_NAME` を使用します。
  return env.state.INPUT.messages.slice(-1)[0].content;
}
```

### LLMを使用してユーザーの入力を処理

```javascript
You're a link extractor, which extracts http or https links from given text, output the result as a json format, output contains two fields, first is link, which contains the link extracted from text, second is language, which contains language code of given question.
Here's the given text, let's begin:
{{EXTRACT_QUESTION}}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // 前のアクションの出力を参照するために `env.state.Action_NAME` を使用します。
  const output = JSON.parse(env.state.REFINE.completion.text);
  // linkが存在する場合、そのlinkを出力
  // linksが存在する場合、最初の要素を出力
  return {
    link: output.link ? output.link : (output.links ? output.links[0] : ""),
    language: output.language ?? 'en'
  };
}
```

### `WEB_CRAWL Action`を使用して情報を収集

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  let content = env.state.WEB_CRAWL_1.data ? env.state.WEB_CRAWL_1.data[0].results[0].text.slice(0, 3000) : "";
  content = content.replace(/\n/g, ""); // 改行を削除
  return {
    content: content,
  };
}
```

### Webページの内容をLLMに送信

```javascript
Your role is that of a text editor. 
You are expected to peruse the texts provided to you, comprehending them fully, and then distill and summarize them for me. The summary should encapsulate the main theme and essential details of the original text. It should be succinct and expressed in your own words. 
The contents that need to be summarized will be enclosed within three single quotation marks.
 
The summary should be conducted in accordance with the following regulations:
1. Thematic Statement: Succinctly summarize the main theme or key point of the original text. 
2. Key Details: Enumerate the crucial details or facts from the original text that support the main theme or point. 
3. Overall Conclusion: Distill the conclusion of the original text or the position of the author.
 
Please organize the summary according to the following structure and reply me:
Introduction: Introduce the main theme or background of the original text.(New line)
Body Paragraph: List and explain the key details and arguments from the original text, summarizing them in your own words. (New line)
Conclusion: Summarize the main points of the original text or present the author's conclusion.(New line)
 
This is the content that requires summarization:

please reply to me with the phrase: "I apologize for being unable to retrieve content from the URL you provided. Please verify the correctness of the web address"
 
{{CODE_1.content}}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // 前のアクションの出力を参照するために `env.state.Action_NAME` を使用します。
  return {
    role: "assistant",
    content: env.state.OUTPUT_STREAM.completion.text,
    retrievals: env.state.RETRIEVALS
  };
}
```

### 最終結果の出力

```javascript
// 最終結果を出力するためのコード片
_fun = (env) => {
  return {
    role: "assistant",
    content: env.state.FINAL_OUTPUT.content,
    retrievals: env.state.FINAL_OUTPUT.retrievals
  };
}
```

## まとめ

以上の手順を通じて、ウェブページの内容を要約するエージェントを作成することができます。このエージェントは、ユーザーから提供されたURLを読み