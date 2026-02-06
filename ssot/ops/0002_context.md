# Project Context（経緯・分離・現在モード）

## 分離（役割）
- vrmmo-ssot: 設定（SSoT）の正本。整理・整備はここで行う。
- vrmmo-novel: 小説本文の消費側（SSoTを参照して書く）。設定整理はここで行わない。

## 経緯（要点）
- 目的：AIが実在MMO常識で暴走しない。未定義を勝手に確定しない。参照の再現性を上げる。
- 参照の固定：SSOT_LOCK で ssot_repo / ssot_tag を固定し、タグはスナップショット参照に使う。
- legacy/monolith_frozen は「移行元の凍結参照」として扱い、直接編集の正本にはしない。

## 現在の作業モード
- mode = ssot_organize（設定整理）
- このモードでは：執筆をしない／新規設定の確定をしない（必要ならBacklog化）
## Ownership Note
- Delegation: SSOT_LOCK / ssot_tag の更新手順は ssot/ops/0004_release_protocol.md を正本とする。
