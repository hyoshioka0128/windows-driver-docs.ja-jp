---
title: bpid
description: Bpid 拡張機能では、ターゲット コンピューター上のプロセスは、デバッガーまたはユーザー モード デバッガーがターゲット コンピューター上のプロセスに接続されている要求によって分割を要求します。
ms.assetid: 47091651-3b39-4e3d-86cf-a8e95779a025
keywords:
- Windows デバッグ bpid
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bpid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5bfa8a179571bd4f61ad6b11618eb4def71ecbab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539116"
---
# <a name="bpid"></a>! bpid


**! Bpid**拡張機能は、ターゲット コンピューター上のプロセスは、デバッガーまたはユーザー モード デバッガーがターゲット コンピューター上のプロセスに接続されている要求によって分割を要求します。

```dbgcmd
    !bpid [Options] PID 
```

## <a name="span-idddkbpiddbgspanspan-idddkbpiddbgspanparameters"></a><span id="ddk__bpid_dbg"></span><span id="DDK__BPID_DBG"></span>パラメーター


<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *オプション*   
このコマンドの追加のアクティビティを制御します。

有効な値*オプション*次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-</strong></p></td>
<td align="left"><p>指定されたプロセスに新しいユーザー モード デバッガーをアタッチ<em>PID</em>します。 ユーザー モード デバッガーは、ターゲット コンピューターで実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong></p></td>
<td align="left"><p>ユーザー モードで中断する直前に、WinLogon プロセスで発生するブレークポイントを追加で指定されたプロセス<em>PID</em>します。 これにより、ユーザーがアクションを試行する前に、要求を確認できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-w</strong></p></td>
<td align="left"><p>ターゲット コンピューターのメモリ内の要求を格納します。 ターゲット システムでは、要求を繰り返すことができますし、これは通常必要ありません。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
ターゲット コンピューターで、目的のプロセスのプロセス ID を指定します。 この対象のコンピューターにユーザー モード デバッガーの制御に使用する場合*PID*ユーザー モード デバッガーのではありません、ターゲット アプリケーションのプロセス ID である必要があります。 (プレフィックスにする必要がありますので、プロセス Id は、10 進数形式で表示されます、通常は、 **0n**または 16 進形式に変換します)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

この拡張機能のコマンドは、x86 ベース、x64 ベースおよび Itanium ベースのターゲット コンピューターでサポートされます。

<a name="remarks"></a>注釈
-------

このコマンドは、入力とカーネル デバッガーに、ユーザー モード デバッガーから出力をリダイレクトしたときに特に便利です。 さらに、カーネル デバッガーからの入力を要求するユーザー モード デバッガーを中断するユーザー モードの対象アプリケーションが発生します。 参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。

ユーザー モードが呼び出しを処理する別の状況でこのコマンドを使用する場合**DbgBreakPoint**します。 これは、カーネル デバッガーに直接、通常は中断されます。

**-S**オプションでは、指定されたプロセスの中断が発生する直前に WinLogon で、中断をされます。 これは、winlogon プロセスのプロセスのコンテキスト内でのデバッグ操作を実行する場合に便利です。 [ **G (移動)** ](g--go-.md) 2 つ目の中断に移動するコマンドを使用し、できます。

この拡張機能が実行に失敗することができる方法があることに注意してください。

-   リソースの不足。 **! Bpid**拡張機能では、システムがスレッドを作成するのに十分なリソースをいる必要がありますので、ターゲット プロセスにスレッドを挿入します。 使用して、 **-a**オプションには、以降のさらに多くのシステム リソースが必要です。 **! bpid-a**ターゲット コンピューターに、デバッガーの完全なインスタンスを実行する必要があります。

-   ローダー ロックが既に保持されています。 両方 **! bpid**と **! bpid-a**にするには、ターゲット プロセスで実行するスレッドを必要としてデバッガーを中断します。 別のスレッドでローダー ロックが保持している場合、 **! bpid**スレッドを実行することにすることはできませんし、デバッガーにブレークが発生します。 したがって場合、 **! bpid**ユーザー モードのメモリ不足がターゲット プロセスの使用可能な場合に、失敗は、ローダー ロックが保持されていることができます。

-   権限がないです。 操作、! bpid 拡張機能には、リモートのスレッドを作成し、特定のプロセスにデバッガーをアタッチする WinLogon のための十分なアクセス許可が必要です。

-   Ntsd.exe にアクセスできません。 一般的な既知のパスを ntsd.exe が見つからない場合。 bpid を適切な PID を設定するには失敗します。 Windows Vista では既定でその ntsd.exe が含まれていないに注意してください。

 

 





