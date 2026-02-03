# SSoT Constitution（憲法）

## North Star（目的）
- AIが実在MMO常識で暴走しない
- 現実MMOの妥当性チェックは「類推」として扱う（確定扱いしない）
- 設定矛盾を最小化し、執筆支援の再現性を上げる

## Non-Goals（非目的）
- 未定義を勝手に確定しない（類推と確定を区別）
- 物語の都合で仕様を歪めない（必要ならBacklogへ）

## SSoT（唯一の正）
- 正は ssot/ 配下のファイル集合
- 入口は次の3つ：
  - ssot/ROUTER.yml
  - ssot/MANIFEST.yml
  - ssot/ops/0000_constitution.md（本書）

## 参照ポリシー
- クリックリンク（#anchor）禁止
- 参照は （**参照**：ID...） のようなID参照のみ（乱発しない）
- 未決/TBDは CANON/DICT に混入させず Backlog へ隔離

## 変更フロー（提案→採用→反映）
- 反映はユーザーの採用後のみ（採用意思が無い限り反映しない）
- 採用決定は Decisions、履歴は Changelog に残す

## 回答フォーマット（ドリフト防止）
- 冒頭で必ず宣言：
  - intent（今回の依頼タイプ）
  - 参照宣言（実際に読んだファイル一覧）
  - North Star整合（1行）

## DRIFT STOP（強制復帰）
ユーザーが「DRIFT STOP」または「ドリフト」と言ったら作業を停止し、以下だけ返す：
- intent再判定
- 入口ファイルの参照宣言（ROUTER根拠）
- いまズレている点（1～3点）
- 以降の再提案（A/B/C）
