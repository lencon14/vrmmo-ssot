# \# DR-2026-02-07: ssot\_organize 項番再構築（体系優先 / 大改造許容）

# 

# \## 状況 / 背景

# \- 目的：巨大な設定を分割し、ゼロから再採番できる体系を作る。

# \- 優先：最小リスクや現状維持より、長期の整合性・監査性・AIの判断精度を最大化する。

# \- ただし「未来の構造を先に決め過ぎる」リスクを下げるため、先に“不変条件”を固定する。

# 

# \## 決定（Decision）

# \### D1. 採番方式：多階層ID（可変深さ）

# \- IDは 2階層以上の多階層を許容（例：DOMAIN.XX\[.XX...].YYY）

# \- 深さは固定しない（2〜N）。必要になれば細分化できる。

# \- 例（表記は概念。実装時に厳密な文法を定義する）：

# &nbsp; - SYS.02.001（戦闘コア）

# &nbsp; - SYS.02.01.001（ダメージ詳細）

# &nbsp; - WLD.01.001（勢力・地域）

# 

# \### D2. IDの生涯ルール（不変）

# \- 一度発行したIDは再割当しない（廃止は deprecated と redirect で表現）。

# \- path（配置）や章構造が変わってもIDは維持する。

# 

# \### D3. 構造の正本：番号ではなく MANIFEST

# \- “番号＝構造”に依存しない。

# \- 親子関係（parent/children）や並び順は MANIFEST 側を正本とし、構造変更はMANIFEST編集で吸収する。

# 

# \### D4. MANIFEST：v2へ（メリット最大化）

# \- MANIFESTを version: 2 に更新し、機械可読な管理項目を追加する。

# \- 追加（最低限）：

# &nbsp; - files\[].id

# &nbsp; - files\[].parent（または parent\_id）

# &nbsp; - files\[].status（shell|active|legacy|deprecated）

# &nbsp; - files\[].owner\_ref（ownership正本への参照キー）

# \- 互換性最大化のため、既存の項目（path/domain/title/keywords等）は可能な限り維持する。

# 

# \### D5. owner宣言：一元管理（正本は ownership\_matrix）

# \- ownerの正本は ownership\_matrix（または同等の単一台帳）に置く。

# \- 各ドキュメントはownerを重複記載しない（必要なら owner\_ref のみ）。

# 

# \### D6. ROUTER：intentを増やして誘導精度を優先

# \- 迷子防止とAIの誤参照抑止のため、intentを増やす。

# \- ただし初期は中核 intent に限定し、運用しながら増やす。

# 

# \### D7. 既存ドキュメント移行：最終的に採番体系へ統合（rename/move含む）

# \- 最終形は新体系（ID中心）に収束させる。

# \- ただし移行順は制御する（入口→SYSTEMコア→その他→大規模rename/move）。

# 

# \## ガードレール（破綻防止）

# \- G1: MANIFEST v2 化は互換性監査（既存スクリプトの前提確認）を先に行う。

# \- G2: IDは不変。構造変更はMANIFESTの親子編集で吸収する。

# \- G3: ownerは一元台帳のみを正とし、二重管理を禁止する。

# \- G4: 入口（ROUTER/Index）を先に固め、混在期間でも参照の正しさを担保する。

# \- G5: PRは「互換性の土台 → 殻 → 移行」の順。1目的1PR。

# 

# \## 移行の優先順位（推奨）

# 1\) ROUTER・Index（入口）

# 2\) SYSTEMコア（戦闘・成長・UI/UX等）

# 3\) WORLD/CHAR/ITEM/LORE

# 4\) 最後に大規模rename/move（LEGACY対応表とredirectを整備した後）

# 

# \## 非目標（このDRではやらない）

# \- 世界設定（数値・固有名・正史）の確定

# \- 小説本文の執筆

# \- 未読の推測での補完

# 

# \## 参照

# \- 正本固定は vrmmo-novel/SSOT\_LOCK.yml@main の ssot\_tag を唯一の正とする。

# \- 参照は ssot\_tag で固定された内容のみを根拠とする。

# 

