---
title: "Raycast AI Commandで日々の文章作成を効率化する実践テクニック"
emoji: "✨"
type: "tech"
topics: ["Raycast", "AI", "生産性"]
published: false
publication_name: "raycast_jp"
---

# Raycast AI Commandで日々の文章作成を効率化する実践テクニック

## はじめに
こんにちは！Raycast日本コミュニティの[矢野](https://x.com/nagauta_jp)です。
最近はRaycastが日常に溶け込みすぎて、どの機能がRaycastによるものか忘れてしまうことに悩んでいます。
今年は特にRaycast AI Commandsにハマっており、書いた文章の整形やフォーマット変更を瞬時に行えるのが本当に便利だと感じています。
本稿では、僕が実際に日常的に使っているRaycast AI Commandの活用事例を紹介します。

## Raycast AI Commandとは？
Raycast AI Commandは、Raycast内でAIを活用できる機能です。
テキストの選択、変換、生成を自然言語で指示できます。

![](/images/raycast-ai-commands/raycast-ai-hero.png)


### 主な特徴
- システム全体で使える（どのアプリからでも呼び出せる）
- カスタムコマンドの作成が可能
- 複数のAIモデルに対応

## よく使う文章整形のユースケース

### 1. 箇条書きを表形式に変換
議事録やメモを箇条書きで書いた後、表形式に整形したい時によく使います。
例えば開発をしていると設計に悩むことがあり一度言語化して整理することがあります。
例としてプロジェクトのリポジトリ構成に悩んでいると仮定してみます。

**Before:**

```
プロジェクトのリポジトリ構成をどうするか悩んでいる。
フロントエンド、ミドルウェア、バックエンドの3つのコンポーネントがあって、
monorepoにするかpolyrepoにするか決めないといけない。
小規模で素早い反復開発を優先するならmonorepoが良さそうだし、
大規模で安定性を重視するならpolyrepoかな。
GoogleやFacebookはmonorepo派だけど、うちのチームの規模だとどっちが適切なんだろう。
今後の成長も考えないといけないし、CI/CDパイプラインの調整も必要になるよな...
```

**使用するコマンド:**
`Convert to Markdown Table`

このコマンドを使用するには`Create AI Command`を使用して下記を設定します
```
{argument name="指示" default=""}
please convert following input into markdown table
{selection}
```

表の構成や整理したい内容は、入力する文章の内容や前提の文脈によって異なります。
そのため、任意の引数で追加の指示を入れられるようにしています。
対象の文章を選択して作成したコマンドを実行すると下記のような文章が生成されます。
AIモデルは品質重視で`Claude 4.5 Sonnet`にしています。

![](/images/raycast-ai-commands/raycast-ai-command-1.png)

**After:**

`# リポジトリ構成の悩み - 観点整理`

| 観点 | Monorepo | Polyrepo | 備考 |
|:---|:---|:---|:---|
| **適した規模** | 小規模チーム | 大規模チーム | チームの現在規模と将来の成長を考慮 |
| **開発速度** | 素早い反復開発に適している | 安定性重視の開発に適している | プロジェクトの優先事項による |
| **コンポーネント** | フロントエンド・ミドルウェア・バックエンドを一元管理 | 各コンポーネントを独立管理 | 3つのコンポーネント構成 |
| **採用企業例** | Google、Facebook | - | 大企業の事例 |
| **CI/CDパイプライン** | 統合的な設定が必要 | 各リポジトリで個別設定 | どちらも調整が必要 |
| **将来の拡張性** | スケールに課題が出る可能性 | スケールしやすい | 今後の成長を見据えた判断が必要 |
| **コード共有** | 容易 | 複雑（パッケージ管理が必要） | 共通コードの扱い |
| **依存関係管理** | 一元管理 | 個別管理 | バージョン管理の複雑さ |

`## 検討すべきポイント`

* 現在のチーム規模と今後3-5年の成長予測
* 開発スピードと安定性のどちらを優先するか
* CI/CDパイプラインの構築・運用コスト
* コンポーネント間の依存関係の強さ
* チームメンバーのスキルセットと学習コスト

このように、整理されていなかった思考が表形式で可視化され、比較検討しやすくなりました。AIの力を借りることで、思考の整理が進み、意思決定の材料が明確になります。

### 2. 英作文を添削する
SlackやGitHubで英語でコミュニケーションを取る際、文法や誤字をチェックするのに便利です。
Raycastにデフォルトで用意されているコマンドで、選択した英文を添削してくれます。
特にSlackで海外の方と半ば同期的にやり取りするときに毎回翻訳アプリを経由すると遅いのでこのコマンドが重宝しています。

![](/images/raycast-ai-commands/raycast-ai-command-2.png)


**Before:**
```
It's ok to host meetup on oct 29
```

**使用するコマンド:**
`Fix Spelling and Grammar`

実行すると次のような結果が得られます

![](/images/raycast-ai-commands/raycast-ai-command-3.png)

**After:**
```
It's okay to host a meetup on October 29.
```

文法の間違いや誤字、冠詞の抜けなどを自動で修正してくれます。そのまま上書きして送信できるため、英語でのコミュニケーションがスムーズになります。

### 3. 英語の文章を日本語に、その逆も
ドキュメントやGitHub issueを翻訳する際に頻繁に使用しています。
Raycastを使えば、どのアプリでも選択した箇所を瞬時に翻訳できるのが便利です。

**Before:**

`このPRでは、ユーザー認証機能を実装しました。JWTトークンを使用したセッション管理と、リフレッシュトークンの自動更新機能を追加しています。`

このコマンドを使用するには`Create AI Command`を使用して下記を設定します
```
Translation Rules

STEP 1: Language Detection
- First, identify the input language
- Japanese text → Translate to English
- English text → Translate to Japanese
- If mixed languages are present, identify the primary language

STEP 2: Translation Guidelines

When translating Japanese → English:
- Translate into natural and fluent English
- Choose appropriate expressions based on context
- Use formal language for business documents, natural colloquial expressions for casual text

When translating English → Japanese:
- Translate into natural and readable Japanese
- Preserve the original nuance and intent
- Use appropriate levels of politeness (keigo) based on context

Other Languages:
- If the input is neither Japanese nor English, specify the language before translating

Output Format
- Output only the translation
- No explanations or annotations (unless there's a special reason)
- Preserve line breaks and paragraph structure from the original text

{selection}
```

実行すると次のような結果が得られます

![](/images/raycast-ai-commands/raycast-ai-command-4.png)

**After:**
`This PR implements user authentication. It adds session management using JWT tokens and an automatic refresh token update feature.`

入力言語を自動判別し、適切な言語に翻訳してくれます。AIモデルは速度と品質のバランスが良かったため`Gemini 2.5 Flash Lite`にしています。
