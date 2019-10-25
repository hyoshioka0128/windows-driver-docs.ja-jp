---
title: 診断とデバッグ
description: 診断とデバッグ
ms.assetid: 6c5c1b4a-338d-4550-903d-c6905ce743f9
keywords:
- RDBSS WDK ファイルシステム、診断
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、診断
- 診断 WDK RDBSS
- ドライバーのデバッグ WDK RDBSS
- ドライバーのデバッグ WDK RDBSS
- RDBSS WDK ファイルシステム、デバッグ
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、デバッグ
- 追跡 WDK RDBSS の逆参照
- 参照追跡 WDK RDBSS
- アサートルーチン WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 484432e171a57afcf37a8ab0c160000067eb70e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841437"
---
# <a name="diagnostics-and-debugging"></a>診断とデバッグ


## <span id="ddk_diagnostics_and_debugging_if"></span><span id="DDK_DIAGNOSTICS_AND_DEBUGGING_IF"></span>


RDBSS には、診断およびデバッグのための多くのルーチンが用意されています。 これらのルーチンは、次の2つのカテゴリに分類されます。

-   アサートルーチンとデバッグルーチン

-   参照と逆参照の追跡ルーチン

これらのルーチンには、次の表に示す項目が含まれます。

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
<td align="left"><p>このルーチンは、RDBSS のチェックされたビルドでアサート文字列をカーネルデバッガーに送信します (インストールされている場合)。 RxAssert インクルードファイルを使用すると、この<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert)"><strong>rxAssert</strong></a>ルーチンも呼び出されるように Windows カーネルの<strong>rtlassert</strong>呼び出しが再定義されます。</p>
<p>リテールビルドの場合、このルーチンの呼び出しによってバグチェックが行われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>このルーチンは、カーネルデバッガーによって処理される例外を発生させます (カーネルデバッガーがインストールされている場合)。それ以外の場合は、デバッグシステムによって処理されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference)"><strong>Rxp Track逆参照</strong></a></p></td>
<td align="left"><p>このルーチンは、チェックされたビルドで、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB、SRV_OPEN の各構造体を参照する要求を追跡するために使用されます。 これらの参照要求のログは、ログ記録システムおよび WMI からアクセスできます。 このルーチンは、逆参照操作を実行しません。</p>
<p>リテールビルドの場合、このルーチンは何も行いません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference)"><strong>Rxp Trackreference</strong></a></p></td>
<td align="left"><p>このルーチンは、チェックを行うビルドで、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB、SRV_OPEN の各構造を逆参照する要求を追跡するために使用されます。 これらの逆参照要求のログは、ログ記録システムおよび WMI からアクセスできます。 このルーチンでは、参照操作は実行されません。</p>
<p>リテールビルドの場合、このルーチンは何も行いません。</p></td>
</tr>
</tbody>
</table>

 

前の表に示したルーチンに加えて、これらのルーチンを呼び出す多くのマクロがデバッグ用に定義されています。 次の表に記載されているこれらのマクロは、 [**RxReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference)または[**RxDereference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)ルーチンのラッパーを提供しています。これらのルーチンは、SRV\_呼び出し、Net\_ROOT、V\_net\_root でのファイル構造管理操作に使用されます。FOBX、FCB、および SRV\_開いている構造体。 これらのマクロは、対応する**RxReference**または**RxDeference**ルーチンを呼び出す前に、対応する[**Rxp Trackreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference)または[**rxp track逆参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference)ルーチンを呼び出して診断情報をログに記録します。 参照要求と逆参照要求のログには、RDBSS logging システムと WMI からアクセスできます。

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
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb、RxContext</em>、 <em>RecursiveFinalize</em>、 <em>forcefinalize</em>)</p></td>
<td align="left"><p>このマクロは、FCB 構造体での逆参照操作を追跡するために使用されます。</p>
<p>このマクロは参照カウントを操作し、finalize 呼び出しの状態も返すことに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>このマクロは、FCB 構造体での逆参照操作を追跡するために使用されます。</p>
<p>このマクロは参照カウントを操作し、最後の逆参照呼び出しの状態も返すことに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceNetFobx</strong> (<em>fobx, LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロは、FOBX 構造体での逆参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetRoot</strong> (<em>netroot</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロは、NET_ROOT 構造体の逆参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceSrvCall</strong> (<em>srvcall</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロは、SRV_CALL 構造体の逆参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceSrvOpen</strong> ( <em>srvopen</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロは、SRV_OPEN 構造体の逆参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceVNetRoot</strong> ( <em>vnetroot</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>このマクロは、NET_ROOT 構造体の逆参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>このマクロは、FCB 構造体に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>fobx</em>)</p></td>
<td align="left"><p>このマクロは、FOBX 構造体の参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>netroot</em>)</p></td>
<td align="left"><p>このマクロは、NET_ROOT 構造体の参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>srvcall</em>)</p></td>
<td align="left"><p>このマクロは、DPC レベルではない SRV_CALL 構造体に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>srvcall</em>)</p></td>
<td align="left"><p>このマクロは、DPC レベルで SRV_CALL 構造体に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>srvopen</em>)</p></td>
<td align="left"><p>このマクロは、SRV_OPEN 構造体の参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>vnetroot</em>)</p></td>
<td align="left"><p>このマクロは、V_NET_ROOT 構造体の参照操作を追跡するために使用されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




