---
title: スレッドの構文
description: スレッドの構文
ms.assetid: f3eaa0ee-7c4f-47a4-aba9-c1d21c1529d1
keywords:
- スレッド、コマンドの構文
- ~ (スレッド id)
- スレッド、スレッド識別子 (~)
- スレッド、スレッド ID
- ~ (スレッド id)
- コマンドの構文規則 ~ (スレッド id)
- コマンドの構文規則 ~ (スレッド id)
- スレッドのコマンドの構文規則
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed9b36168fc29b13fbe732662dc4ba2aeea26941
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551051"
---
# <a name="thread-syntax"></a>スレッドの構文


## <span id="ddk_thread_syntax_dbg"></span><span id="DDK_THREAD_SYNTAX_DBG"></span>


多くのデバッガー コマンドでは、そのパラメーターとしてスレッドの識別子を持ちます。 スレッド識別子の前にチルダ (~) が表示されます。

スレッド識別子には、次の値のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">スレッドの識別子</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>~.</strong></p></td>
<td align="left"><p>現在のスレッド。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~#</strong></p></td>
<td align="left"><p>現在の例外のデバッグ イベントの原因となったスレッドです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>~*</strong></p></td>
<td align="left"><p>プロセスのすべてのスレッド。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~</strong><em>数</em></p></td>
<td align="left"><p>インデックスがあるスレッド<em>数</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>~~</strong>[<em>TID</em>]</p></td>
<td align="left"><p>スレッド id を持つスレッド<em>TID</em>します。 (角かっこは必須と 2 番目のパラメーターがチルダとかっこの間にスペースを追加することはできません)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>~</strong>[<em>式</em>]</p></td>
<td align="left"><p>スレッドのスレッド ID が、整数を数値<em>式</em>を解決します。</p></td>
</tr>
</tbody>
</table>

 

作成されるとき、スレッドはインデックスに割り当てられます。 この番号は異なるスレッド ID、Microsoft Windows オペレーティング システムを使用することに注意してください。

デバッグの開始時に現在のスレッドが存在する例外やデバッグ イベント (または、プロセスにデバッガーがアタッチされている場合は、アクティブ スレッド) の原因となった 1 つにします。 使用して、新しいものを指定するまで、スレッドが現在のスレッドが変更される、 [ **~ s (現在のスレッドの設定)** ](-s--set-current-thread-.md)コマンドまたはを使用して、[プロセスとスレッド ウィンドウ](processes-and-threads-window.md)WinDbg でします。

スレッドの識別子は、通常コマンドのプレフィックスとして表示されます。 すべてのワイルドカード文字はスレッド識別子を使用するすべてのコマンドで使用できることに注意してください。

例、~\[*式*\]構文になります`~[@$t0]`します。 この例では、スレッドは、ユーザー定義の擬似レジスタの値によって変わります。 この構文ではデバッガーのスクリプトをプログラムでスレッドを選択します。

### <a name="span-idcontrollingthreadsinkernelmodespanspan-idcontrollingthreadsinkernelmodespancontrolling-threads-in-kernel-mode"></a><span id="controlling_threads_in_kernel_mode"></span><span id="CONTROLLING_THREADS_IN_KERNEL_MODE"></span>カーネル モードでのスレッドを制御します。

カーネル モードでは、スレッド識別子を使用してスレッドを制御できません。 カーネル モードでスレッド固有の情報にアクセスする方法の詳細については、[変更コンテキスト](changing-contexts.md)を参照してください。

**注**  チルダ (~) を使用して、ユーザー モードのデバッグ中にスレッドを指定することができます。 カーネル モードのデバッグは、プロセッサを指定するのにチルダを使用することができます。 プロセッサを指定する方法の詳細については、[マルチプロセッサ構文](multiprocessor-syntax.md)を参照してください。

 

 

 





