<!--
title:   【LINE Notify】LINE Notifyのステータスを確認する
tags:    GAS,GoogleAppsScript,LineNotify,Python
id:      80f8b94fc1a12d7c6525
private: true
-->

# はじめに

LINE Notifyのトークンのステータスを確認できるそうです。
公式ドキュメント↓

https://notify-bot.line.me/doc/ja/

これに関する記事が見つからなかったので書いてみました。

# 1.レスポンスの内容

メッセージ本文にJSONとして詳細な情報が記載されます。
レスポンス本文はJSONのobject型になります。

```
{"status":200,"message":"ok","targetType":"GROUP","target":"NotifyTest"}
```

![response](image/23/02/22/response.png)

既にグループを抜けている場合は以下のようなレスポンスが返ってきます。

```
{"status":200,"message":"ok","targetType":"GROUP","target":null}
```

一応メッセージは送ることは可能です。

# 2.Pythonで確認

requestsモジュールが必要です。
ない場合は以下のコマンドでインストールしてください。

```
pip install requests
```

```python:main.py
import requests


line_access_token = 'トークン'
headers = {'Authorization': 'Bearer ' + line_access_token}
r = requests.get('https://notify-api.line.me/api/status', headers=headers)
print(r.text)
```

```
'{"status":200,"message":"ok","targetType":"GROUP","target":"グループ名"}'
```

# 3.GASで確認

```javascript:main.gs
function myFunction() {
  const headers = {
    'Authorization': 'Bearer ' + 'トークン'
  };

  const options = {
    'method': 'GET',
    'headers': headers
  };

  const response = JSON.parse(UrlFetchApp.fetch('https://notify-api.line.me/api/status', options).getContentText());
  console.log(response);
}
```
