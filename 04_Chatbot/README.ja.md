# ラボ 4-会話型インターフェイス (チャットボット)

## [概要]

チャットボットやバーチャルアシスタントなどの会話型インターフェースを使用して、顧客のユーザーエクスペリエンスを向上させることができます。チャットボットは、自然言語処理 (NLP) と機械学習アルゴリズムを使用してユーザーのクエリを理解し、それに応答します。チャットボットは、顧客サービス、営業、電子商取引などのさまざまなアプリケーションで使用でき、ユーザーに迅速かつ効率的に対応できます。Web サイト、ソーシャルメディアプラットフォーム、メッセージングアプリなど、さまざまなチャネルからアクセスできます。

## Amazon Bedrock を使用するチャットボット

![Amazon Bedrock - Conversational Interface](./images/chatbot_bedrock.png)

## ユースケース

1.  **Chatbot (Basic)**-FM モデルのゼロショットチャットボット
2.  **Chatbot using prompt**-テンプレート (Langchain)-プロンプトテンプレートにコンテキストが提供されているチャットボット
3.  **Chatbot with persona**-役割が定義されたチャットボット。例：キャリアコーチとヒューマンインタラクション
4.  **Contextual-aware chatbot**-埋め込みを生成して外部ファイルにコンテキストを渡します。

## Amazon Bedrockでチャットボットを構築するためのラングチェーンフレームワーク

チャットボットのような会話型インターフェースでは、短期的にも長期的にも、以前のやりとりを覚えておくことが非常に重要です。

LangChainは2つの形式のメモリコンポーネントを提供します。まず、LangChain には以前のチャットメッセージを管理および操作するためのヘルパーユーティリティが用意されています。これらはモジュール式で、使用方法に関係なく便利に使えるように設計されています。第二に、LangChain はこれらのユーティリティをチェーンに組み込む簡単な方法を提供しています。
さまざまなタイプの抽象化を簡単に定義して操作できるため、強力なチャットボットを簡単に構築できます。

## コンテキストを活用したチャットボットの構築-主な要素

コンテキスト認識型チャットボットを構築する最初のプロセスは、コンテキストを **generate embeddings** にすることです。通常は、埋め込みモデル全体を通して埋め込みを生成する取り込みプロセスを経て、一種のベクターストアに格納されます。この例では、GPT-J 埋め込みモデルを使用しています。

![Embeddings](./images/embeddings_lang.png)

2 番目のプロセスは、ユーザーリクエストのオーケストレーション、インタラクション、結果の呼び出しと返却です。

![Chatbot](./images/chatbot_lang.png)

## アーキテクチャ [コンテキスト認識型チャットボット]

![4](./images/context-aware-chatbot.png)

このアーキテクチャでは:

1.  LLMに尋ねられた質問は、埋め込みモデルにまで及びます
2.  コンテキストドキュメントは [アマゾンタイタン埋め込みモデル](https://aws.amazon.com/bedrock/titan/) を使用して埋め込まれ、ベクターデータベースに保存されます。
3.  次に、埋め込まれたテキストがFMに入力され、コンテキスト検索とチャット履歴が含まれます。
4.  その後、FM モデルはコンテキストに基づいて結果を表示します。

## ノートブック

このモジュールは、同じパターンのノートブックを2冊提供します。アマゾン・タイタン・テキスト・ラージだけでなく、アントロピック・クロードとの会話も体験でき、それぞれのモデルの会話力を体感できます。

1.  [クロードを使ったチャットボット](./00_Chatbot_Claude.ipynb)
2.  [Titan を使用するチャットボット](./00_Chatbot_Titan.ipynb)