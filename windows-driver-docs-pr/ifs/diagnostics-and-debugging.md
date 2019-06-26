---
title: 診断とデバッグ
description: 診断とデバッグ
ms.assetid: 6c5c1b4a-338d-4550-903d-c6905ce743f9
keywords:
- RDBSS WDK ファイル システムでは、診断
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、診断
- WDK RDBSS の診断
- ドライバー WDK RDBSS のデバッグ
- ドライバー WDK RDBSS のデバッグ
- RDBSS WDK ファイル システム、デバッグ
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、デバッグ
- WDK RDBSS の追跡を逆参照します。
- 参照の WDK RDBSS の追跡
- WDK RDBSS ルーチンをアサートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6f7489a7e8776640c30e47bd42455d8887e2105
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386097"
---
# <a name="diagnostics-and-debugging"></a>診断とデバッグ


## <span id="ddk_diagnostics_and_debugging_if"></span><span id="DDK_DIAGNOSTICS_AND_DEBUGGING_IF"></span>


RDBSS は、診断とデバッグのためのさまざまなルーチンを提供します。 これらのルーチンは、2 つのカテゴリに分類されます。

-   アサートして、デバッグ ルーチン

-   参照し、追跡ルーチンを逆参照

これらのルーチンには、次の表に、項目が含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert)"><strong>RxAssert</strong></a></p></td>
<td align="left"><p>このルーチンは、インストールされている場合、カーネル デバッガーに RDBSS のチェックで、assert 文字列ビルドを送信します。 RxAssert.h が含まれる場合は、ファイルが使用される、Windows カーネル<strong>RtlAssert</strong>呼び出しはこれを再定義する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert)"> <strong>RxAssert</strong> </a>ルーチンもします。</p>
<p>製品版ビルドでは、このルーチンの呼び出しはチェックをバグします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>このルーチンは、インストールされている場合は、カーネル デバッガーによって処理される例外を発生させます。それ以外の場合、デバッグ、システムによって処理されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackdereference" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackdereference)"><strong>RxpTrackDereference</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX FCB を参照する要求を追跡するために使用し、チェックで SRV_OPEN 構造を構築します。 これらの参照要求のログは、ログ記録システムおよび WMI でアクセスできます。 このルーチンは、逆参照操作を実行できません。</p>
<p>製品版ビルドでは、このルーチンは何もしません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackreference" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackreference)"><strong>RxpTrackReference</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX FCB、逆参照する要求を追跡するために使用し、チェックで SRV_OPEN 構造を構築します。 これらのログの要求を逆参照のログ記録システムと WMI によってアクセスできます。 このルーチンは、参照操作を実行できません。</p>
<p>製品版ビルドでは、このルーチンは何もしません。</p></td>
</tr>
</tbody>
</table>

 

前の表に、ルーチンに加え、いくつかのマクロをこれらのルーチンを呼び出すは、デバッグに対して定義されます。 次の表に示されている、これらのマクロのラッパーを提供する、 [ **RxReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxreference)または[ **RxDereference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdereference)ルーチンSRV 上のファイル構造管理操作のために使用される\_呼び出し、NET\_ルート, V\_NET\_ルート、FOBX、FCB、SRV、\_オープン構造体。 これらのマクロが最初に、対応するを呼び出す[ **RxpTrackReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackreference)または[ **RxpTrackDereference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackdereference)診断ログに記録するルーチンについては、対応するを呼び出す前に**RxReference**または**RxDeference**ルーチン。 A は、参照のログし、要求を逆参照 RDBSS ログ システムと WMI によってアクセスできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb、RxContext</em>、 <em>RecursiveFinalize</em>、 <em>ForceFinalize</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 FCB 構造での操作を逆参照します。</p>
<p>このマクロは、参照カウントを操作し、finalize 呼び出しの状態を返しますに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 FCB 構造での操作を逆参照します。</p>
<p>このマクロは、参照カウントを操作し、最終的な逆参照呼び出しの状態を返しますに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceNetFobx</strong> (<em>Fobx,LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 FOBX 構造での操作を逆参照します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetRoot</strong> (<em>NetRoot</em>、 <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 NET_ROOT 構造での操作を逆参照します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceSrvCall</strong> (<em>SrvCall</em>、 <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 SRV_CALL 構造での操作を逆参照します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceSrvOpen</strong> ( <em>SrvOpen</em>、 <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 SRV_OPEN 構造での操作を逆参照します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceVNetRoot</strong> ( <em>VNetRoot</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 NET_ROOT 構造での操作を逆参照します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>このマクロは、FCB 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>Fobx</em>)</p></td>
<td align="left"><p>このマクロは、FOBX 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>NetRoot</em>)</p></td>
<td align="left"><p>このマクロは、NET_ROOT 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>このマクロは、DPC レベルでない SRV_CALL 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>このマクロは、DPC レベル SRV_CALL 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>SrvOpen</em>)</p></td>
<td align="left"><p>このマクロは、SRV_OPEN 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>VNetRoot</em>)</p></td>
<td align="left"><p>このマクロは、V_NET_ROOT 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




