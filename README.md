# Yuya Hirata

LLMの推論基盤からRAG・AIエージェントまで、LLMシステムの構築と選定に取り組んでいます。

技術選定は感想ではなく、事前に決めた手順と統計的な検定で決めるようにしています。

## 検証に基づいて選ぶ

- **[vlm-vs-yolo](https://github.com/yuya0408/vlm-vs-yolo)** — 汎用VLMと専用検出器(YOLO)のどちらを採るかを、COCO 300枚で検証。YOLOを既定の閾値のまま比べるとVLMが有意に勝つ(McNemar `p=0.004`)が、閾値を公平に選ぶと有意差は消える(`p=0.71`)。精度が互角なら決め手はコストとレイテンシ、という意思決定ルールまで落とした。<br>
  記事: [前編](https://zenn.dev/yuya0408/articles/yolo-vs-vlm-background) / [後編](https://zenn.dev/yuya0408/articles/yolo-vs-vlm-evaluation-pitfall)
- **[gbrain-embedding-eval](https://github.com/yuya0408/gbrain-embedding-eval)** — RAG基盤の埋め込みモデルを「足切り → Cochran's Q検定 → スループット実測」で選び直した。決勝4モデルに品質の有意差はなく(`p=0.449`)、事前に決めたタイブレーカーで決着。移行後、gbrain本体での検索MRRは`0.336 → 0.676`。<br>
  記事: [Zenn](https://zenn.dev/yuya0408/articles/gbrain-embedding-eval)

## LLM推論基盤・OSS

- **vllm-mlx** — 推論エンジンが生成に失敗したとき、エラーではなく空の応答を返していた不具合を修正。<br>
  [PR #825](https://github.com/waybarrios/vllm-mlx/pull/825)(マージ済み)
- **[エラーを出さずにDGX Sparkが2台とも固まった ― 原因はmodel.train()の呼び忘れ](https://zenn.dev/yuya0408/articles/gb10-unified-memory-oom-hang)** — 分散学習中のハングを、ドライバのメモリ挙動まで追って切り分けた記録

## MLモデルを運用に乗せる

- **[secom-defect-prediction](https://github.com/yuya0408/secom-defect-prediction)** — 半導体製造データの不良予測を、リークを排除した評価(AUC `0.72 → 0.61`)から、FastAPI+Dockerでのサービス化、3層のドリフト監視と再学習の線引きまで。<br>
  記事: [考察編](https://zenn.dev/yuya0408/articles/secom-defect-analysis) / [実装編](https://zenn.dev/yuya0408/articles/secom-defect-serving) / [運用編](https://zenn.dev/yuya0408/articles/secom-defect-operations) ・ デモ: [Hugging Face Spaces](https://huggingface.co/spaces/yuya-h/secom-defect-demo)

## Links

[Zenn](https://zenn.dev/yuya0408)
