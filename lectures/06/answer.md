# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：glossary_search_glossary
- STEP 2 の [tool call]：[tool call]   glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]：[tool call]   fetch_fetch({'url': 'https://modelcontextprotocol.io/'})
- STEP 4 の [tool call]：[tool call]   aws_aws___search_documentation({'search_phrase': 'Amazon S3 versioning overview', 'topics': ['general']})
- 気づき・疑問：
  MCPサーバーを利用することで、エージェント本体を変更せず、設定ファイルへの追記だけで外部ツールを利用できることが分かった。また、ローカルで起動するサーバーと外部で稼働するサーバーの接続方法の違いを確認できた。業務で利用する場合は、外部への情報送信やツールのアクセス範囲にも注意が必要だと感じた。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：
  app/mcp_server.py に server.tool()(tools.get_lecture_summary) を1行追加し、既存の講義概要取得関数をMCPツールとして公開した。
- 結果：
  「第2回では何を学びますか？」と質問したところ、以下のツールが呼び出され、第2回の講義概要に基づく回答が得られた。

  [tool call]   glossary_get_lecture_summary({'lecture': 2})

  モデル応答回数は2回だった。また、pytestによるテストは21件すべて成功した（21 passed in 4.38s）。
  ツール一覧に glossary_get_lecture_summary が追加され、モデルから利用可能なツールが合計8個となったことを確認した。
- 気づき・疑問：
  エージェント側のコードや接続設定を変更することなく、サーバー側に1行追加するだけで新しいツールを利用できることを確認した。ツールの提供側と利用側を分離することで、機能の追加や保守が容易になると感じた。
