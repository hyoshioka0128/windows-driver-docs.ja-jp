---
title: RDBSS で定義されたマクロ
description: RDBSS で定義されたマクロ
ms.assetid: 11add885-ecd9-4b43-be42-ef060e847183
keywords:
- RDBSS WDK ファイルシステム、マクロ
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、マクロ
- マクロ WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6482e5ca8c25c9053f55b2db6734795661f607e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841132"
---
# <a name="macros-defined-by-rdbss"></a>RDBSS で定義されたマクロ


## <span id="ddk_macros_defined_by_rdbss_if"></span><span id="DDK_MACROS_DEFINED_BY_RDBSS_IF"></span>


便利なマクロの多くは、これらの RDBSS ルーチンやその他のカーネルルーチンを呼び出す Windows Driver Kit (WDK) ヘッダーファイルで定義されています。 これらのマクロの一部は、通常、RDBSS ルーチンを直接呼び出す代わりに使用されます。 これらのマクロの一部は、便利なルーチンとして使用されます。

次のマクロは、RDBSS で定義されています。

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
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> (<em>テーブル</em>、<em>待機</em>)</p></td>
<td align="left"><p>このマクロは、変更操作のために、排他モードでプレフィックステーブルロックを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> (<em>テーブル</em>、<em>待機</em>)</p></td>
<td align="left"><p>このマクロは、参照操作のために、共有モードでプレフィックステーブルロックを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> (<em>type</em>、 <em>size</em>、 <em>tag</em>)</p></td>
<td align="left"><p>Checked ビルドでは、このマクロは、メモリ trashing のインスタンスをキャッチするために使用できる、ブロックの先頭に4バイトのタグがあるプールからメモリを割り当てます。</p>
<p>リテールビルドでは、このマクロは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>Exallocatepoolwithtag</strong></a>への直接の呼び出しになります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>Checked ビルドでは、このマクロはメモリブロックに特別な RX_POOL_HEADER HEADER 署名があるかどうかをチェックします。</p>
<p>リテールビルドでは、このマクロは何も行いません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb、RxContext</em>、 <em>RecursiveFinalize</em>、 <em>forcefinalize</em>)</p></td>
<td align="left"><p>このマクロは、FCB 構造体での逆参照操作を追跡するために使用されます。</p>
<p>このマクロは参照カウントを操作し、最後の逆参照呼び出しの状態も返すことに注意してください。</p></td>
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
<td align="left"><p>このマクロは、V_NET_ROOT 構造体の逆参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>、 <em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードの通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong>(<em>__ devobj</em>, <em>__ fa</em>)</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a>を呼び出して、通常のディスパッチ i/o ベクターと同一の高速 i/o ディスパッチベクターを入力し、渡されたデバイスオブジェクトに関連付けられた driver オブジェクトにインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFreePool</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>チェックされたビルドでは、このマクロはメモリプールを解放します。</p>
<p>リテールビルドでは、このマクロは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>Exfreepool</strong></a>への直接の呼び出しになります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードの通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが排他モードで通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードまたは排他モードで通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a>ルーチンと<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> (<em>テーブル</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックステーブルロックが排他的モードまたは共有モードのいずれかで取得されたかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> (<em>テーブル</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックステーブルロックが排他モードで取得されたかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLog</strong>(<em>Args</em>)</p></td>
<td align="left"><p>チェックされたビルドでは、このマクロは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a>ルーチンを呼び出します。</p>
<p>リテールビルドでは、このマクロは何も行いません。</p>
<p><strong>RxLog</strong>への引数は、ログ記録をオフにする必要がある場合に null 呼び出しに変換できるようにするために、追加のかっこのペアで囲む必要があることに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>、 <em>id</em>、 <em>EventId</em>、 <em>Status</em>)</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>、 <em>id</em>、 <em>EventId</em>、 <em>Status</em>)</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>,、" <em>"、"</em> <em>"、"</em><em>状態</em>"、"<em>バッファー</em>の長さ"、"<em>長さ</em>なし")</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogRetail</strong>(<em>Args</em>)</p></td>
<td align="left"><p>チェックされたビルドでは、このマクロは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a>ルーチンを呼び出します。</p>
<p>リテールビルドでは、このマクロは何も行いません。</p>
<p><strong>RxLogRetail</strong>への引数は、ログ記録をオフにする必要がある場合に null 呼び出しに変換できるようにするために、追加のかっこのペアで囲む必要があることに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>このマクロは、FCB 構造体に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>fobx</em>)</p></td>
<td align="left"><p>このマクロは、FOBX 構造体の参照操作を追跡するために使用されます。 これらの参照操作のログは、ログ記録システムおよび WMI からアクセスできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>netroot</em>)</p></td>
<td align="left"><p>このマクロは、NET_ROOT 構造体の参照操作を追跡するために使用されます。 これらの参照操作のログは、ログ記録システムおよび Windows Management Instrumentation (WMI) からアクセスできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>srvcall</em>)</p></td>
<td align="left"><p>このマクロは、遅延プロシージャ呼び出し (DPC) レベルではない SRV_CALL 構造体に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>srvcall</em>)</p></td>
<td align="left"><p>このマクロは、DPC レベルで SRV_CALL 構造体に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>srvopen</em>)</p></td>
<td align="left"><p>このマクロは、SRV_OPEN 構造体の参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>vnetroot</em>)</p></td>
<td align="left"><p>このマクロは、V_NET_ROOT 構造体の参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> (<em>テーブル</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックステーブルロックを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>、<em>FCB</em>、<em>ioqueue</em>)</p></td>
<td align="left"><p>このマクロは、ブロッキング i/o 要求を同じ作業キューに同期します。 Windows Server 2003 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>FALSE</strong>に設定して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a>ルーチンを呼び出します。</p>
<p>Windows XP および Windows 2000 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>FALSE</strong>に設定して<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>、<em>FCB</em>、<em>ioqueue</em>)</p></td>
<td align="left"><p>このマクロは、ブロッキング i/o 要求を同じ作業キューに同期します。 Windows Server 2003 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>TRUE</strong>に設定して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a>ルーチンを呼び出します。</p>
<p>Windows XP および Windows 2000 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>TRUE</strong>に設定して<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a>ルーチンを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 




