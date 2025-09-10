```markdown
# 手触り感のあるContext Engineering - LayerX エンジニアブログ 内容整理

---

## 概要
- 著者：LayerX CEO室 AI Agent開発PdM、Kenta Watanabe氏
- LLM（大規模言語モデル）の急速な発展に伴い、プロダクション環境での安定稼働のための試行錯誤がエンジニアの間で課題に。
- 今年6月頃から「Context Engineering」という技術分野が注目され、LLMを効果的に活用、安定稼働させるための手法が整理・体系化されつつある。
- 本記事はContext Engineeringの概要と、実際の開発現場でどのように試行錯誤を行うかを具体例を交えて紹介。

---

## 1. Context Engineeringとは何か？
- もともとはPrompt Engineeringが注目されていたが、一つのLLM呼び出しに対するPrompt調整だけでなく、LLMをプログラムの文脈で安定稼働させるための一連の技術群を指す。
- Shopify CEOや元OpenAI研究者Karpathy氏らがTwitterで発信し話題に。
- 複数のSub Agentに処理を切り分けたり、メインAgentが結果をまとめたりするマルチエージェント設計例も紹介されている。
- AnthropicsのMulti-agentリサーチやhumanlayerの12-factor agentsなど、LLM活用開発をプロダクション品質にするための知見が共有されている。
- ManusやChromaなどもContext Engineeringに関する技術レポートを公開し、多様な技術トピックが活発に議論中。

---

## 2. Context Engineeringの課題と現場の試行錯誤
- 大きなタスクをそのままLLMに投げる（naive実装）は成功率・性能面で問題が多い。
  - 例：経費申請のルール文書からクエリに関連する文を位置付きで抽出する課題を例示。
  - 単純に全てLLMに任せると処理コスト・レイテンシが非常に高く（16kトークン、5分以上）、結果のムラも大きい。
- LLM特性を踏まえタスクを細分化し、得意な部分だけLLMに任せる設計が重要。
  - 具体例としては、「関連文の抽出はLLMに任せ、文字列位置の特定は決定論的コードで行う」ことで安定化を図る。
- Deep ResearchやClaude Citationsの既存ツールは日本語対応や抽出の精度・制御が課題で、実運用には向かないことが判明。
- GoogleのLangExtract（非構造データから構造化データ抽出）は良い参考例として紹介。
  - LLMで抽出した文字列が完全一致しないことを考慮し、fuzzyマッチングや複数回抽出してリコール向上など工夫を行っている。

---

## 3. Context Engineeringの具体的ステップ
- 大きな問題を小さなサブタスクに分解し、LLMに与えるタスクの範囲を限定する。
- Prompt Engineering（LLM出力の望ましい制御）を実験的かつ評価データセットを用いながら継続的に行う。
- LLMの「得意・不得意」を経験的に理解し、LLMの確率的挙動を踏まえてソフトウェア設計をする。
- LLMのtoken生成のレイテンシも考慮し、効率的なトークン数利用やKVキャッシュの活用も重要。
- 複数LLM呼び出しを組み合わせるマルチエージェント構成を設計する際は、ソフトウェア責務の切り分けではなく、LLMのContext制限に配慮した分割が必要。

---

## 4. LLMの能力と限界
- LLMは確率的挙動を持ち、モデル毎に異なるため出力の再現性・安定性確保は課題。
- 100%確実に正確な出力を期待するのは難しい。
- したがって、LLMの弱点はdeterministicなコードや補助的な処理でカバーし、安定動作を目指す設計思想が重要。

---

## 5. LayerXでのLLM活用への姿勢と募集
- LayerXはLLM前提の経済活動デジタル化・摩擦解消に真剣に取り組み、AI Agentの開発を推進中。
- LLM活用に関連した知見共有や課題解決の試行錯誤を継続している。
- 興味を持つ開発経験者・PdM含む幅広いメンバーを積極的に募集。
- AI・LLMは急速に進化し、知見の蓄積も少ない分野であるため、好奇心と試行錯誤精神を持つ人材を歓迎。

---

## 参考リンク
- LayerX AIエージェントブログリレー  
  https://layerx.notion.site/6975c0901ea54ca9b609fafc3e8a35c3?v=268cdd370bae80cc8dfb000c55400a25  
- Shopify CEO @tobiのツイート  
  https://x.com/tobi/status/1935533422589399127  
- Karpathyのツイート  
  https://x.com/karpathy/status/1937902205765607626?lang=en  
- cognition @walden_yan ブログ  
  https://cognition.ai/blog/dont-build-multi-agents#principles-of-context-engineering  
- Anthropic Multi-agent記事  
  https://www.anthropic.com/engineering/multi-agent-research-system  
- humanlayer GitHub「12-factor agents」  
  https://github.com/humanlayer/12-factor-agents  
- Manusブログ（KVキャッシュ活用）  
  https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus  
- Chroma研究レポート「context-rot」  
  https://research.trychroma.com/context-rot  
- Google LangExtract GitHub  
  https://github.com/google/langextract  

---

## まとめ
- Context Engineeringは、LLMを単に使うだけでなく、LLMの強みと弱みを理解しながらタスク分割やPrompt設計、補完的なコード実装で安定稼働実現を目指す総合的な技術。
- LLM処理の不確実性やパフォーマンス面の課題をソフトウェア的工夫でカバー。
- 新しい技術領域で未経験者にも参加の余地が大きく、共に課題解決に挑む仲間を求めている。

---

# 以上
```