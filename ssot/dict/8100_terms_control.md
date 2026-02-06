# DICT Terms Control（用語統制：草案）
- 禁止語／推奨語／言い換え／メタ語彙ガード

## Terms control workflow

この節は「用語統制の運用手順」だけを定義する（プロセス専用）。
世界設定・物語設定・未確定事項を新規に決めない。

### 原則（Adopt-only）
- 未読や未確定を推測で埋めない。
- “正本” は `vrmmo-novel/SSOT_LOCK.yml@main` の `ssot_tag`。判断根拠は **その ssot_tag 固定で到達できるファイル**のみ。
- 不明点は canon 化せず、Issue を backlog / blocked に送る。

### 変更の入口（Issue-first）
用語の追加/変更/廃止/表記ゆれ統合は、必ず Issue から始める。

Issue には最低限これを含める：
- `ssot_tag:` （参照固定点）
- evidence paths: （該当箇所の repo path 群）
- 変更対象:
  - term: <対象用語>
  - action: add | rename | alias | deprecate | split | merge
  - rationale: （推測禁止。根拠ファイルへの参照を優先）

### 採用ルール（互換性）
- rename の場合：旧用語は直ちに消さず、当面は alias / deprecated として残す。
  - “置換先（replacement）” を明記する。
- 表記ゆれ統合：canonical（正規表記）を 1 つに固定し、その他は alias に寄せる。
- 廃止：deprecated にし、replacement（後継）または “no replacement” を明示する。

### 反映手順（SSoT更新）
採用が決まったら、必要最小限の変更のみ行う：
1) `ssot/dict/8100_terms_control.md` に追記/更新（プロセス・辞書エントリのみ）
2) 参照側の文書を更新する場合も、必ず Issue に evidence を残してから行う
3) `vrmmo-ssot` で commit
4) snapshot tag を切る
5) `vrmmo-novel/SSOT_LOCK.yml@main` の `ssot_tag` を更新
6) `dg_recover.ps1` が `DG_RECOVER: SUCCESS` になるまで進めない

## Ownership Note
- Owner: 用語統制（命名/aliases/forbidden/canonical）の規則は本書を正とする。
- Delegation: Issue-first / Adopt-only / status:next は ssot/ops/0003_change_protocol.md を正本とする。
- Delegation: ssot_tag / SSOT_LOCK 更新は ssot/ops/0004_release_protocol.md を正本とする。
