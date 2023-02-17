【GAS】GASからGitHub Actionsを実行してみる

# はじめに

GitHub Actions
GitHub Actionsのドキュメントを見ていたところ、ワークフローを実行させるイベントの中に```repository_dispatch```というものが存在することを知りました。

https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#repository_dispatch

「これ使えば外部から実行できんじゃね？」と思ったので試してみました。
