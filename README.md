# Yuya Hirata

LLMの推論基盤からRAG・AIエージェントまで、LLMシステムの構築に取り組んでいます。

推論エンジンの仕組みを理解したうえで作り・直し、作ったものは評価で良し悪しを判断しています。

## LLM推論基盤・OSS

- **[toolcall-serving-bench](https://github.com/yuya0408/toolcall-serving-bench)** — 同じ8Bモデル(Qwen3-8B)を、NVIDIA L4 1台で5つの推論エンジンと量子化の組み合わせに載せ、ツール呼び出しの精度とレイテンシを測った。精度で足切りしてGPUの台数から構成を選び、その選定を左右した要因(プリフィルの重さ・量子化の計算の形・エンジンの既定値)を特定した。律速はプリフィルの計算で、速さの差はエンジンの違いより、量子化がプリフィルまで軽くするかで付いた。
- **[vLLM・SGLang・TensorRT-LLMをクラウドGPUで動かしたら、それぞれの個性が見えてきた](https://zenn.dev/yuya0408/articles/llm-serving-engines-on-l4)** — 同じモデル・同じGPU(NVIDIA L4)・同じリクエストでも、入力・量子化・容量・溢れたときの動き・観測の5か所で条件が揃わないことを、3エンジンを動かして確かめた記録
- **[vllm-mlx](https://github.com/waybarrios/vllm-mlx)** — 推論エンジンが生成に失敗したとき、エラーではなく空の応答を返していた不具合を修正。<br>
  [PR #825](https://github.com/waybarrios/vllm-mlx/pull/825)(マージ済み)

## AIエージェントの遅れ・失敗を切り分ける

- **[agent-latency-tracer](https://github.com/yuya0408/agent-latency-tracer)** — 自作のAIエージェント・MCPサーバ・RAG(pgvector)・vLLMをBedrock AgentCore Runtimeに載せ、OpenTelemetryの1本のトレースで遅れ・失敗の原因を切り分けた。温めたセッションの1問35.2秒のうち基盤の部品は約1秒で、基盤に固有の問題6件(SDKの自動再送による2重処理、切断後も続く生成など)は、速さより失敗・後始末・監視の見え方に出た。

## 評価で選ぶ

- **[vlm-vs-yolo](https://github.com/yuya0408/vlm-vs-yolo)** — 汎用VLMと専用検出器(YOLO)のどちらを採るかを、COCO 300枚で検証。YOLOが既定の閾値のままだとVLMが有意に上だが(McNemar `p=0.004`)、VLMのスコアを使わずに閾値を選び直すと差を検出できなくなる(`p=0.71`)。精度で決められないときに、コスト・処理量・語彙で選ぶ基準までまとめた。<br>
  記事: [前編](https://zenn.dev/yuya0408/articles/yolo-vs-vlm-background) / [後編](https://zenn.dev/yuya0408/articles/yolo-vs-vlm-evaluation-pitfall)
- **[gbrain-embedding-eval](https://github.com/yuya0408/gbrain-embedding-eval)** — 個人用RAGの埋め込みモデル6候補を「足切り → Cochran's Q検定 → スループット実測」で選び直した。上位4モデルの品質差は検出できず(`p=0.449`)、スループットで決めた。既定のモデルからの移行で、gbrain本体の検索MRRは`0.336 → 0.676`。<br>
  記事: [Zenn](https://zenn.dev/yuya0408/articles/gbrain-embedding-eval)

## MLモデルを運用に乗せる

- **[secom-defect-prediction](https://github.com/yuya0408/secom-defect-prediction)** — 半導体製造データの不良予測。リークを除くとAUCは`0.72 → 0.61`に下がる。その実力で使える範囲を決め(上位50%を検査すると再現率66.2%)、FastAPI+Dockerでの推論API化とドリフト監視の実演まで行った。<br>
  記事: [考察編](https://zenn.dev/yuya0408/articles/secom-defect-analysis) / [実装編](https://zenn.dev/yuya0408/articles/secom-defect-serving) / [運用編](https://zenn.dev/yuya0408/articles/secom-defect-operations) ・ デモ: [Hugging Face Spaces](https://huggingface.co/spaces/yuya-h/secom-defect-demo)

## Links

[Zenn](https://zenn.dev/yuya0408)
