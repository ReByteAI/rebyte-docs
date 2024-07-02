# Bilibili字幕エージェント

Bilibiliの字幕を取得し、コンテンツを要約するのに役立ちます。

### `Datasets`でテストデータを設定

```json
[
  {
    "role": "user",
    "content": "BV1Lu411J7Z8"
  }
]
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
  return env.state.INPUT.messages.slice(-1)[0].content
}
```

### ユーザーの入力を処理するためにLLMを使用

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
 return env.state.GET_BV.completion.text
}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
 return env.state.GET_BV.completion.text
}
```

### `Http Request Maker`を使用してCIDをリクエスト

```javascript
api.bilibili.com/x/player/pagelist?bvid={{BV}}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
 return env.state.GET_CID.body.data[0].cid
}
```

### `Http Request Maker`を使用して字幕のURLをリクエスト

```javascript
api.bilibili.com/x/player/v2?bvid={{BV}}&cid={{CID}}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
  // const data = JSON.stringify(env.state.GET_URL.body)
  // const regex = /<subtitle>(.*?)<\/subtitle>/;
  // const match = data.match(regex);
  // const subtitleURL = match ? match[1] : "";
  // const obj = subtitleURL.replace(new RegExp("\\\\\"","gm"),"\"")
  // const result = JSON.parse(obj)['subtitles'][0]['subtitle_url'].replace("//", "")
  const url = env.state.GET_URL.body.data.subtitle.subtitles[0].subtitle_url;
  const result = url.replace(/\/\//g, "");
  return result;
}
```

### `Http Request Maker`を使用して字幕をリクエスト

```javascript
{{GET_CC_URL}}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
  let arr = [];
  for(let i in env.state.GET_CC.body.body) {
    arr.push(env.state.GET_CC.body.body[i].content);
  }
  return arr.join(',');
}
```

### 字幕をLLMに送信して要約
```json
{% if GET_URL.body.data.subtitle.subtitles[0].subtitle_url == "" %}
please reply to me with the phrase: "I apologize for being unable to retrieve content from the URL you provided. Please verify the correctness of the web address"

{% else %}
You are an AI with advanced comprehension and summarization skills. Your task is to read the following passage and provide a concise, clear summary that captures the main points and key details. 

Passage: 
{{CC}}

Please provide a summary of the above passage and respond to me in Chinese.

{% endif %}
```

### `Code Action`からコンテンツを抽出

```javascript
_fun = (env) => {
  // `env.state.Action_NAME`を使用して前のアクションの出力を参照します。
 return {
   role: "assistant",
   content: env.state.OUTPUT_STREAM.completion.text,
   retrievals: env.state.RETRIEVALS
 }
}
```

### 最終結果を出力