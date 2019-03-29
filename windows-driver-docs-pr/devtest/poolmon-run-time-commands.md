---
title: PoolMon のランタイム コマンド
description: PoolMon の実行中には、表示を変更するには、実行時のコマンドを使用します。
ms.assetid: 834f406d-5e5d-416e-90df-b52b61d70ea7
keywords:
- PoolMon ランタイムのドライバーの開発ツールをコマンドします。
topic_type:
- apiref
api_name:
- PoolMon Run-time Commands
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa05117519f0d8f87b20a32da6a03b346c2b305
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578908"
---
# <a name="poolmon-run-time-commands"></a>PoolMon のランタイム コマンド


PoolMon の実行中には、表示を変更するには、実行時のコマンドを使用します。 各実行時のコマンドは、1 つのキーボード文字で構成されます。 コマンドを実行するキーを押します。

```
    [p] [( | )] [s] [TSSessionID] [i] [l] [e] [t] [a] [f] [d] [b] [m] [h | ?] [q | ESC]
```

## <a name="span-idddkpoolmonruntimecommandstoolsspanspan-idddkpoolmonruntimecommandstoolsspanparameters"></a><span id="ddk_poolmon_run_time_commands_tools"></span><span id="DDK_POOLMON_RUN_TIME_COMMANDS_TOOLS"></span>パラメーター


<span id="_______p______"></span><span id="_______P______"></span> **p**   
非ページ割り当てやページの割り当ての表示を切り替えます。

<span id="_________or__"></span><span id="_________OR__"></span> **(** または **)**  
(割り当て、無料の操作およびバイト) 値で並べ替えと並べ替えの値を変更して表示を切り替えます。 いずれかのかっこ文字を使用することができます。 同じ効果があります。

<span id="_______s______"></span><span id="_______S______"></span> **s**   
システム プールと、ターミナル サービス セッションのプールの表示を切り替えます。

<span id="_______TSSessionID______"></span><span id="_______tssessionid______"></span><span id="_______TSSESSIONID______"></span> *TSSessionID*   
指定されたターミナル サービス セッションのプールから割り当てを表示します。 *TSSessionID*ターミナル サービス セッションのセッション ID を表します。 0 ~ 9 の整数の可能性があります。 セッションのすべてのプールを表示する、またはセッション Id が 9 よりも大きい値を入力するには、使用、**は**コマンド。

<span id="_______i______"></span><span id="_______I______"></span> **i**   
ターミナル サーバー セッションのセッション ID を求められます。 次の 2 つの方法で応答することができます。

-   ターミナル サービス セッションのすべてのプールから割り当てを表示するには、ENTER キーを押します。

-   特定のターミナル サービス セッション プールから割り当てを表示するには、セッション ID を入力し、し、ENTER キーを押します。

<span id="_______l______"></span><span id="_______L______"></span> **l**   
オンとオフの変更された行の強調表示を切り替えます。

<span id="_______e______"></span><span id="_______E______"></span> **e**   
プールの合計のオンとオフを切り替えます。 ディスプレイ画面の下部に合計が表示されます。

<span id="_______t______"></span><span id="_______T______"></span> **t**   
タグ名を基準に並べ替えます。

<span id="_______a______"></span><span id="_______A______"></span> **A**   
割り当ての数を基準に並べ替えます。 かっこ文字を使用すると、 **、** 割り当ての変更でキーを並べ替えます。

<span id="_______f______"></span><span id="_______F______"></span> **f**   
無料の操作の数を基準に並べ替えます。 かっこ文字を使用すると、 **f**無料操作の変更でキーを並べ替えます。

<span id="_______d______"></span><span id="_______D______"></span> **D**   
割り当てられたバイト数と解放されるバイトの差を基準に並べ替えます。

<span id="_______b______"></span><span id="_______B______"></span> **b**   
使用されているバイトを基準に並べ替えます。 かっこ文字を使用すると、 **b**キー サイズをバイト単位で変更順に並べ替えます。

<span id="_______m______"></span><span id="_______M______"></span> **m**   
バイトの割り当てごとに並べ替えます。 かっこ文字を使用すると、 **m**バイト-ごとの割り当ての変更でキーを並べ替えます。

<span id="_________or_h"></span><span id="_________OR_H"></span> **?** または**h**  
スタートアップ コマンドのパラメーター、実行時のコマンドは、および PoolMon 表示の説明が表示されます。 ヘルプを表示を閉じるには、ESC キーを押します。

<span id="_______q_or_ESC"></span><span id="_______q_or_esc"></span><span id="_______Q_OR_ESC"></span> **q**または**ESC**  
PoolMon を停止します。









