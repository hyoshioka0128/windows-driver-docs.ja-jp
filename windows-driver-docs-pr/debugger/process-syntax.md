---
title: プロセスの構文
description: プロセスの構文
ms.assetid: fe08b5fe-ec27-4264-baee-de4c11bcb2bf
keywords:
- プロセスでは、コマンドの構文
- (プロセス id)
- プロセス、プロセス識別子)
- プロセス、プロセス ID (PID)
- PID (プロセス ID)
- (プロセス id)
- (プロセス id)、コマンドの構文規則
- (プロセス id)、コマンドの構文規則
- プロセス識別子)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e300706debbbbfae9bc08aa15acef5c07e8c0412
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537390"
---
# <a name="process-syntax"></a>プロセスの構文


## <span id="ddk_process_syntax_dbg"></span><span id="DDK_PROCESS_SYNTAX_DBG"></span>


多くのデバッガー コマンドでは、そのパラメーターとしてプロセスの識別子を持ちます。 縦棒 (|) は、プロセス識別子の前に表示されます。

プロセス識別子には、次の値のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プロセス識別子</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>|.</strong></p></td>
<td align="left"><p>現在のプロセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|#</strong></p></td>
<td align="left"><p>現在の例外のデバッグ イベントの原因となったプロセス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>|*</strong></p></td>
<td align="left"><p>すべてのプロセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|</strong><em>数</em></p></td>
<td align="left"><p>プロセスの序数<em>数</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>| ~ [</strong><em>PID</em><strong>]</strong></p></td>
<td align="left"><p>プロセス id を持つプロセス<em>PID</em>します。 (角かっこは必須およびティルダ (~) と角かっこの間にスペースを追加することはできません)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|[</strong><em>式</em><strong>]</strong></p></td>
<td align="left"><p>プロセスのプロセス ID が、整数を数値<em>式</em>を解決します。</p></td>
</tr>
</tbody>
</table>

 

作成されるときのプロセスには序数が割り当てられます。 この番号は異なるプロセス ID (PID)、Microsoft Windows オペレーティング システムを使用することに注意してください。

現在のプロセスでは、メモリ領域と使用されるスレッドのセットを定義します。 デバッグの開始時に、現在のプロセスが存在する例外やデバッグ イベント (または、デバッガーにアタッチするプロセス) が発生したにします。 使用して、新しいものを指定するまで、プロセスが現在のプロセスが変更される、 [ **| s (現在のプロセスの設定)** ](-s--set-current-process-.md)コマンドまたはを使用して、[プロセスとスレッド ウィンドウ](processes-and-threads-window.md)WinDbg で.

プロセス id は、コマンドの先頭として頻繁にいくつかのコマンドのパラメーターとして使用されます。 WinDbg および CDB が元のプロセスが作成された子プロセスをデバッグできますに注意してください。 WinDbg および CDB は、また複数の関連のないプロセスにアタッチできます。

例、|\[*式*\]構文になります\[|@$t0\]します。 この例では、プロセスは、ユーザー定義の擬似レジスタの値によって変わります。 この構文ではデバッガーのスクリプトをプログラムでプロセスを選択します。

### <a name="span-idcontrollingprocessesinkernelmodespanspan-idcontrollingprocessesinkernelmodespancontrolling-processes-in-kernel-mode"></a><span id="controlling_processes_in_kernel_mode"></span><span id="CONTROLLING_PROCESSES_IN_KERNEL_MODE"></span>カーネル モードでプロセスを制御します。

カーネル モードでは、プロセスの識別子を使用してプロセスを制御できません。 カーネル モードでプロセスに固有の情報にアクセスする方法の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

 

 





