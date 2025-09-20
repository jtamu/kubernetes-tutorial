# Podのスケジューリング

## 概要

- スケジューリングとは
    - どのNodeにどのPodを配置するかを制御すること
- なぜスケジューリングする必要があるのか
    - せっかくPodを複数立てていても、全て同じNodeに配置していた場合そのNodeに障害が起こると全てのPodがダウンしてしまい可用性のメリットが受けられないため

## Node selector

特定のNodeにのみスケジュールする
（条件を満たすNodeがない場合はスケジュールしない）

## Affinity / Anti-affinity

### Node affinity

- requiredDuringSchedulingIgnoredDuringExecution
    - 特定の条件を満たすNodeにのみスケジュールする
    - Node selectorとほぼ一緒だが条件指定が柔軟にできる
- preferredDuringSchedulingIgnoredDuringExecution
    - 特定の条件を満たすNodeに対して優先的にスケジュールする
    - weightで重み付けできるため、複数条件がある場合は最も合計値が高いNodeにスケジュールする

### Pod affinity / Pod anti-affinity

- 基本的にNode affinityと同じだが、NodeのラベルではなくPodのラベルに基づいてスケジュールする
- anti-affinityで同じアプリのPodを同じNodeに載せないという指定がよくある使われ方

## Pod Topology Spread Containers

- Pod anti-affinityと同様、Podを分散させるための設定
- 後発なのでより柔軟な指定ができる
    - Pod anti-affinityとは違い、Pod数がNode数を上回る場合でも適切に分散できる
    - maxSkewで許容する各Node上のPod数の差分を設定できる

## Taint / Toleration

- Taint: Nodeに付与できる「汚れ」
- Toleration: Nodeに付与された「汚れ」を「許容」するかどうかのPodの設定
- つまり、Taintが設定されたNodeには、対応するTolerationが設定されたPodのみがスケジュールできる

## Pod Priority / Preemption

- Pod Priorityが設定されていると、全てのPodを配置できない(preemption)場合より優先度の低いPodを押しのけてスケジュールされる
    - Podに直接設定するのではなく、PriorityClassを通じて設定する
