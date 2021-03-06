---
title: RDBSS が定義するマクロ
description: RDBSS が定義するマクロ
ms.assetid: 11add885-ecd9-4b43-be42-ef060e847183
keywords:
- RDBSS WDK ファイル システム、マクロ
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、マクロ
- WDK RDBSS マクロ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c0ba92cd075cf297dc4895e0d2565a2c886df1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375994"
---
# <a name="macros-defined-by-rdbss"></a>RDBSS が定義するマクロ


## <span id="ddk_macros_defined_by_rdbss_if"></span><span id="DDK_MACROS_DEFINED_BY_RDBSS_IF"></span>


いくつかの便利なマクロは、これらの RDBSS ルーチンまたは他のカーネル ルーチンを呼び出すウィンドウ Driver Kit (WDK) のヘッダー ファイルで定義されます。 これらのマクロの一部は RDBSS ルーチンを直接呼び出す代わりに通常使用されます。 これらのマクロの一部は、利便性のためのルーチンとして使用されます。

次のマクロは、RDBSS によって定義されます。

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
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> (<em>TABLE</em>, <em>WAIT</em>)</p></td>
<td align="left"><p>このマクロでは、変更操作の排他モードでプレフィックス テーブル ロックを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> (<em>TABLE</em>, <em>WAIT</em>)</p></td>
<td align="left"><p>このマクロでは、共有モードの検索操作でプレフィックス テーブル ロックを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> (<em>型</em>、<em>サイズ</em>、<em>タグ</em>)</p></td>
<td align="left"><p>チェック済みのビルドでは、このマクロは、メモリの破壊のインスタンスを検出するときに使用できるブロックの先頭 4 バイトのタグを使用して、プールからメモリを割り当てます。</p>
<p>製品版ビルドでは、このマクロが、直接呼び出しを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)"> <strong>exallocatepoolwithtag に</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>チェック済みのビルドでは、このマクロは、特別な RX_POOL_HEADER ヘッダーの署名のメモリ ブロックを確認します。</p>
<p>製品版ビルドでこのマクロは何もしません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb、RxContext</em>、 <em>RecursiveFinalize</em>、 <em>ForceFinalize</em>)</p></td>
<td align="left"><p>このマクロを使用して追跡 FCB 構造での操作を逆参照します。</p>
<p>このマクロは、参照カウントを操作し、最終的な逆参照呼び出しの状態を返しますに注意してください。</p></td>
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
<td align="left"><p>このマクロを使用して追跡 V_NET_ROOT 構造での操作を逆参照します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>, <em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredsharedlite)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong>(<em>__devobj</em>, <em>__fastiodisp</em>)</p></td>
<td align="left"><p>このマクロを呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"> <strong>__RxFillAndInstallFastIoDispatch</strong> </a>通常のディスパッチ I/O ベクターとそれをドライバー オブジェクトに関連付けられているインストールと一致するよう、高速な I/O ディスパッチ ベクターの入力をデバイス オブジェクトが渡されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFreePool</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>チェック済みのビルドでは、このマクロは、メモリ プールを解放します。</p>
<p>製品版ビルドでは、このマクロが、直接呼び出しを<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)"> <strong>ExFreePool</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredsharedlite)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが排他モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredexclusivelite)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有または排他モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredsharedlite)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisresourceacquiredexclusivelite)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックス テーブル ロックが排他的であるか、または共有モードで取得されたかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックスのテーブル ロックを排他モードで取得されたかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLog</strong>(<em>Args</em>)</p></td>
<td align="left"><p>チェック ビルドは、このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog)"> <strong>_RxLog</strong> </a>ルーチン。</p>
<p>製品版ビルドでこのマクロは何もしません。</p>
<p>なお、引数を<strong>RxLog</strong>追加のログ記録をオフにするときに、null の呼び出しに変換を有効にするかっこのペアで囲む必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventdirect)"> <strong>RxLogEventDirect</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventdirect)"> <strong>RxLogEventDirect</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>, <em>_Buffer</em>, <em>_Length</em>)</p></td>
<td align="left"><p>このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"> <strong>RxLogEventWithBufferDirect</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogRetail</strong>(<em>Args</em>)</p></td>
<td align="left"><p>チェック ビルドは、このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog)"> <strong>_RxLog</strong> </a>ルーチン。</p>
<p>製品版ビルドでこのマクロは何もしません。</p>
<p>なお、引数を<strong>RxLogRetail</strong>追加のログ記録をオフにするときに、null の呼び出しに変換を有効にするかっこのペアで囲む必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>このマクロは、FCB 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>Fobx</em>)</p></td>
<td align="left"><p>このマクロは、FOBX 構造に対する参照操作を追跡するために使用されます。 これらの参照操作のログは、ログ記録システムおよび WMI でアクセスできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>NetRoot</em>)</p></td>
<td align="left"><p>このマクロは、NET_ROOT 構造に対する参照操作を追跡するために使用されます。 これらの参照操作のログは、ログ記録システムと Windows Management Instrumentation (WMI) でアクセスできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>このマクロは、遅延プロシージャ呼び出し (DPC) のレベルでない SRV_CALL 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>このマクロは、DPC レベル SRV_CALL 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>SrvOpen</em>)</p></td>
<td align="left"><p>このマクロは、SRV_OPEN 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>VNetRoot</em>)</p></td>
<td align="left"><p>このマクロは、V_NET_ROOT 構造に対する参照操作を追跡するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>このマクロは、プレフィックスのテーブル ロックを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>このマクロは、同じ作業キューにブロッキング I/O 要求を同期します。 Windows Server 2003 では、このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"> <strong>__RxSynchronizeBlockingOperations</strong> </a>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>FALSE</strong>.</p>
<p>Windows XP および Windows 2000 では、このマクロを呼び出し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock)"> <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong> </a>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>FALSE</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>このマクロは、同じ作業キューにブロッキング I/O 要求を同期します。 Windows Server 2003 では、このマクロを呼び出す、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"> <strong>__RxSynchronizeBlockingOperations</strong> </a>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>TRUE</strong>.</p>
<p>Windows XP および Windows 2000 では、このマクロを呼び出し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock)"> <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong> </a>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>TRUE</strong>します。</p></td>
</tr>
</tbody>
</table>

 

 

 




