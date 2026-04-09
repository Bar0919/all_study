# Statistics Mastery - 統計学完全理解

このディレクトリは、統計学の各トピックを「証明」「立式」「実装」の3点セットで完全にマスターすることを目的とします。

## 学習方針

各トピックディレクトリは、以下の3つのファイルで構成されます。

- `logic.md`:
  その統計手法がどのような現実の現象をモデル化しているのか、どのような仮定に基づいているのかといった、論理的な背景と思想を記述します。

- `proof.md`:
  数式（TeX記法を推奨）を用いて、その手法の数学的な導出過程や性質の証明を厳密に記述します。これにより、理論的な正しさを自ら確認します。

- `implementation.py`:
  NumPyなどの基本的なライブラリのみを使い、統計アルゴリズムをスクラッチで実装します。これにより、理論がコードに落ちる過程を深く理解します。

## 学習トピック一覧

- **`01_mean_and_variance`**: 平均と分散
  - [証明](./01_mean_and_variance/proof.md)
  - [立式](./01_mean_and_variance/logic.md)
  - [実装](./01_mean_and_variance/implementation.py)
- **`02_hypothesis_testing`**: 仮説検定
  - [証明](./02_hypothesis_testing/proof.md)
  - [実装](./02_hypothesis_testing/t_test_scratch.py)
- ... more topics to be added.
  - 確率分布
  - ベイズ統計
  - 一般化線形モデル
  - etc.
