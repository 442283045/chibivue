Prev | [Next](https://github.com/Ubugeeei/chibivue/blob/main/books/japanese/02_what_is_vue.md)

---
title: "はじめに"
---

# 🎯 本書の目的

この本を手に取って頂きありがとうございます!  
少しでも興味を持って頂いたということで大変嬉しく思います。  
この本の目的について最初にまとめておきます。

**☆ 目的**

- **Vue.js についての理解を深める**  
  Vue.js とは何なのか? どういう構成で成り立っているのか?
- **Vue.js の基本的な機能を実装できるようになる**  
  実際に基本的な機能を実装してみる
- **vue/core のソースコードを読めるようになる**  
  実装と本家のコードとの関連を把握して、実際にどんな実装になっているのかを把握する

いくつかざっくりした目的を挙げましたが、この全てを満たす必要はないですし、完璧を目指す必要はありません。  
通しで全て読んでもらっても、部分的に読みたいところを読んでもらってもご自由に。。  
少しでも参考になる部分があれば嬉しいです!

# 🤷‍♂️ 想定する対象者

- **Vue.js を触ったことがある**
- **TypeScript が書ける**

以上があれば他の知識は何も必要ありません。  
この本の中では普段聞きなれない言葉がたくさん出てくるかもしれませんが、可能な限り前程知識は排除し、随時説明してこの本内で完結できることを目指します。  
ですが、Vue.js や TypeScript について知らないといった方であれば、まずはそちらの方から学ばれることを推奨します。
(基本的な機能についていればそれで十分です! (詳しくある必要はない))

# 🙋‍♀️ この本(著者)が意識していること (したいこと)

この本を書く上で意識しておきたいことをいくつかまとめておくので、その心構えで読んでいただけると幸いです。
もしも、この点で欠けている点があればご指摘ください。

- **前程知識の排除**  
  前述の「想定する対象者」に関する説明と重複してしまいますが、この本では可能な限り前程知識は排除し、随時説明してこの本内で完結できることを目指します。
  これはより多くの方々にとってわかりやすい説明を広めたいからです。
  ある程度、知識のある方にとっては冗長な説明に感じる部分が多くあるかもしれませんが、その辺はご了承ください orz

- **インクリメンタルな実装**  
  この本の目的の一つとして、Vue.js を自分の手で小さく実装するというのがあります。  
  つまりはこの本は実装ベースで説明をしていくのですが、その際はなるべく小さくインクリメンタルな実装を心がけます。  
  もう少し具体的にいうと、「動かない状態をなるべく減らす」ということです。  
  最後まで完成しないと動かないなどといった実装は避け、なるべく常に成果物が動いている状態を目指します。  
  これは筆者が個人的に何かを実装する上でかなり大切にしていることで、動かないコードを書き続けるのはやはり辛いです。  
  不完全ではあるものの、常に動いているような状況を作ることとで楽しくやっていきましょう。  
  「やった! 次はここまで動くようになった!」というのを小さく繰り返していくようなイメージです!

- **特定のフレームワーク・ライブラリ・言語などの優劣をつけるような内容にはしない**  
  今回は Vue.js を主題として取り上げますが、昨今は他にも素晴らしいフレームワークやライブラリ、言語が多数あります。
  実際、著者も Vue.js 以外でも好きなライブラリ等はたくさんありますし、自分では書かないけれどそれらで作られたサービス・知見にとても助けらることも日常茶飯事です。
  本書の目的はあくまで、「Vue.js について理解する」であり、他の議論はその範囲を超えます。ついてはそれぞれの優劣をつけるような目的は含みません。

# 💡 こので取り上げることと流れ

本書はかなりボリューミーな感じになってしまっているので、各部門ごとに達成マイルストーンを立てて分割します。

- **Minimal Example 部門**  
  最小の構成で Vue.js を実装します。機能としても一番小さい部門ですが、仮想 DOM, リアクティブシステム コンパイラ, SFC の対応を行います。  
  対応といっても実用的なものからは程遠く、かなり簡略化した実装になっています。
  しかし、Vue.js の全体像がどうなっているかのざっくりした理解をしたい方にとっては十分な達成率です。

- **Basic Virtual DOM 部門**  
  ここではある程度実用的な仮想 DOM のパッチレンダリング機能の実装を行います。  
  suspense などの機能や最適化の実装は行いませんが、基本的なレンダリングであれば問題なくできる程度の完成度です。  
  スケジューラの実装もここで行います。

- **Basic Component System 部門**  
  ここでは Component System 関する基本実装を行います。実は、Basic Virtual DOM 部門で Component System のベースは実装してしまうので、
  それ以外の部分の Component System を実装します。例えば props/emit や provide/inject、リアクティブシステムの拡張、ライフサイクルフックなどです。

- **Basic Template Compiler 部門**  
  Basic Virtual DOM で実装した仮想 DOM システムに対応する機能のコンパイラに加え、v-on, v-bind, v-for 等のディレクティブなどの実装を行います。  
  基本的にはコンポーネントの template オプションを利用した実装で、SFC の対応はここではやりません。

- **Basic SFC Compiler 部門**  
  ここではある程度実用的な SFC コンパイラを実装します。  
  Basic Template Compiler 部門で実装した template のコンパイラを活用しつつ、ここでは主に script のコンパイラを実装します。  
  具体的には SFC の script(の default exports)や script setup の実装を行います。  
  ここまでくると触り心地としてはかなり普段の Vue に近づきます。

- **Web Application Essentials 部門**  
  Basic SFC Compiler 部門までである程度実用的な Vue.js の機能を実装できます。  
  しかし、Web アプリケーションを開発するにはまだまだ不十分です。例えばグローバルなステートの管理であったり、router の管理であったりが必要です。  
  この部門ではそういった外部プラグインの実装を行って、「Web アプリケーションを開発する」という視点においてさらに実用的なものを目指します。

## ★ Minimal Example 部門

### Vue.js についてのおさらい

改めて Vue.js がどういうものなのかということを公式ドキュメントの引用を元に触れます。
また、この本の位置付け、公式ドキュメントが触れている内容との違いについても説明します。

### Vue.js を構成する主要な要素

Vue.js 本体を実装するにあたって、そもそも Vue.js のソースコードはどういう部品でどういう構成になっているのかということについて説明します。(リアクティブシステム、コンパイラなど)

### createApp API の実装

このチャプターからは早速実装スタート
「え？そこから作るの? 仮想 DOM とかじゃなくて?」と思われるかもしれませんが、前述にある通りこの本ではインクリメンタルは実装を心がけています。
まずは単純な開発者とのインターフェースを実装して動くような状態を目指します。仮想 DOM 等のシステムは必要になったタイミングで足していく方針です。

### 小さいリアクティブシステムの実装

リアクティブシステムの基本説明や基本実装を行います。  
大きなものや実用的なものは目指しません。

### 小さい仮想 DOM の実装

ルートコンポーネントに小さい仮想 DOM を持たせ、簡単なパッチレンダリングを実装します。
仮想 DOM とは何のために存在して、どういうふうに実装されているかという基本について理解します。

## 小さいコンポーネントシステムの実装

Vue.js の特徴のひとつである、「コンポーネントを使った開発」が行えるようなコンポーネントの機能を実装します。
props や emit といった簡単な API の実装も行います。

### 小さいテンプレートコンパイラの実装

前チャプターで実装した h 関数を template として書けるような開発者インターフェースを実装します。
template -> h 関数(正確には createElement 関数)の簡単なコンパイラを実装します。

### 小さい SFC コンパイラの実装

ここまで小さく実装してきたものを Vue.js の醍醐味でもある`SFC` (Single File Component)で開発できるようにコンパイラを実装します。
vite のプラグインを書きながら、script, template, style が動作するものを目指します。

---

Minimal Example 部門はここまでです。ここまで実装すると概ね以下のようなコードが動作するようになります。

```vue
<script>
import { reactive } from "chibivue";

export default {
  setup() {
    const state = reactive({ message: "Hello, chibivue!", input: "" });

    const changeMessage = () => {
      state.message += "!";
    };

    const handleInput = (e) => {
      state.input = e.target?.value ?? "";
    };

    return { state, changeMessage, handleInput };
  },
};
</script>

<template>
  <div class="container" style="text-align: center">
    <h2>{{ state.message }}</h2>
    <img
      width="150px"
      src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/1200px-Vue.js_Logo_2.svg.png"
    />
    <p><b>chibivue</b> is the minimal Vue.js</p>

    <button @click="changeMessage">click me!</button>

    <br />

    <input @input="handleInput" />
    <p>input value: {{ state.input }}</p>
  </div>
</template>

<style>
.container {
  height: 100vh;
  padding: 16px;
  background-color: #becdbe;
  color: #2c3e50;
}
</style>
```

```ts
import { createApp } from "chibivue";
import App from "./App.vue";

const app = createApp(App);

app.mount("#app");
```

---

## ★ Basic Virtual DOM 部門

- 大きくなりそうなので項目は随時更新

## ★ Basic Component System 部門

大きくなりそうなので項目は随時更新

- provide/inject
- computed api
- watch api
- lifecycle hooks

## ★ Basic Template Compiler 部門

大きくなりそうなので項目は随時更新

- v-on
- v-bind
- v-for
- v-model

## ★ Basic SFC Compiler 部門

大きくなりそうなので項目は随時更新

- SFC の基本
- script setup
- style block

## ★ Web Application Essentials 部門

- router
- store

# 🧑‍🏫 この本に対する意見や質問について

この本に関する質問や意見については可能な限り対応しようと思っています。  
Twitter で声をかけてもらってもいいですし(DM でも TL でも)、リポジトリを公開しているのでそちらの issue 等で投げてもらって問題ないです。  
この本も自分自身の理解も完璧ではないと思っているので、随時ご指摘いただけると嬉しいのと、「この説明がわかりづらい!」などもあれば是非問い合わせて欲しいです。  
少しでも多くの方にわかりやすく、正しい説明を広めたいので、ぜひみなさんと一緒に作り上げていけたらなと思います 👍

https://twitter.com/ubugeeei

https://github.com/Ubugeeei/zenn


Prev | [Next](https://github.com/Ubugeeei/chibivue/blob/main/books/japanese/02_what_is_vue.md)