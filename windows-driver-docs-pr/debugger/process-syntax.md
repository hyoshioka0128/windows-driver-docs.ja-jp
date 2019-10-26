---
title: プロセスの構文
description: プロセスの構文
ms.assetid: fe08b5fe-ec27-4264-baee-de4c11bcb2bf
keywords:
- process、command 構文
- (プロセス識別子)
- プロセス、プロセス識別子 ()
- プロセス、プロセス ID (PID)
- PID (プロセス ID)
- (プロセス識別子)
- コマンドの構文規則 (プロセス識別子)
- コマンドの構文規則 (プロセス識別子)
- プロセス識別子 ()
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72ad2af799f8272e72dd2471bd71544a382c742d
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916221"
---
# <a name="process-syntax"></a>プロセスの構文


## <span id="ddk_process_syntax_dbg"></span><span id="DDK_PROCESS_SYNTAX_DBG"></span>


多くのデバッガーコマンドには、パラメーターとしてプロセス識別子があります。 プロセス識別子の前に縦棒 (|) が表示されます。

プロセス識別子には、次のいずれかの値を指定できます。

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
<td align="left"><p>現在の例外またはデバッグイベントの原因となったプロセス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>|*</strong></p></td>
<td align="left"><p>すべてのプロセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|</strong><em>番号</em></p></td>
<td align="left"><p>序数が<em>Number</em>であるプロセス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>| ~ [</strong><em>PID</em><strong>]</strong></p></td>
<td align="left"><p>プロセス ID が<em>PID</em>であるプロセス。 (角かっこは必須であり、チルダ (~) と左角かっこの間にスペースを追加することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>|[</strong><em>式</em><strong>]</strong></p></td>
<td align="left"><p>プロセス ID が数値<em>式</em>の解決に使用される整数であるプロセス。</p></td>
</tr>
</tbody>
</table>

 

プロセスには、作成時に序数が割り当てられます。 この番号は、Microsoft Windows オペレーティングシステムで使用されているプロセス ID (PID) とは異なることに注意してください。

現在のプロセスでは、メモリ空間と使用されるスレッドのセットを定義します。 デバッグが開始されると、現在のプロセスが、現在の例外またはデバッグイベント (またはデバッガーがアタッチしたプロセス) の原因となったプロセスになります。 このプロセスは、新しいプロセスを指定するまで、[ [ **| s (現在のプロセスの設定)** ](-s--set-current-process-.md) ] コマンドを使用するか、WinDbg の [[プロセスとスレッド] ウィンドウ](processes-and-threads-window.md)を使用して、現在のプロセスのままになります。

プロセス識別子は、いくつかのコマンドのパラメーターとして、多くの場合、コマンドプレフィックスとして使用されます。 WinDbg および CDB では、元のプロセスによって作成された子プロセスをデバッグできることに注意してください。 WinDbg と CDB は、関連付けられていない複数のプロセスにもアタッチできます。

| の例を次に示します。\[*式*\] 構文は | です。\[@ $t 0\]。 この例では、ユーザー定義の擬似レジスタの値に応じてプロセスが変更されます。 この構文を使用すると、デバッガースクリプトでプロセスをプログラムで選択できます。

### <a name="span-idcontrolling_processes_in_kernel_modespanspan-idcontrolling_processes_in_kernel_modespancontrolling-processes-in-kernel-mode"></a><span id="controlling_processes_in_kernel_mode"></span><span id="CONTROLLING_PROCESSES_IN_KERNEL_MODE"></span>カーネルモードでのプロセスの制御

カーネルモードでは、プロセス識別子を使用してプロセスを制御することはできません。 カーネルモードでプロセス固有の情報にアクセスする方法の詳細については、「[コンテキストの変更](changing-contexts.md)」を参照してください。

 

 





