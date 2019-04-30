---
title: カーネル ネットワーク ミニリダイレクターによって実装されるルーチン
description: カーネル ネットワーク ミニリダイレクターによって実装されるルーチン
ms.assetid: bd1a8989-100d-4b7b-9a61-521af6433b00
keywords:
- ミニ-リダイレクター WDK、ルーチンの実装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d839ef5d02349f4a3729cfa2213d4e413d5b046e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344538"
---
# <a name="routines-implemented-by-the-kernel-network-mini-redirector"></a>カーネル ネットワーク ミニリダイレクターによって実装されるルーチン


ネットワークのミニ リダイレクターでは、次のルーチンを実装できます。

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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549838" data-raw-source="[&lt;strong&gt;MRxAreFilesAliased&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549838)"><strong>MRxAreFilesAliased</strong></a></td>
<td align="left"><p>RDBSS では、2 つのファイル制御ブロック (FCB) 構造体が同じファイルを表す場合は、ネットワークのミニ リダイレクターを照会するには、このルーチンを呼び出します。 別の名前 (MS-DOS の短い名前と例については、長い名前) がある同じにするファイルの 2 つの処理時にこのルーチン RDBSS 呼び出しが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549841" data-raw-source="[&lt;strong&gt;MRxCleanupFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549841)"><strong>MRxCleanupFobx</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトの拡張機能の構造を閉じることを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548608" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548608)"> <strong>IRP_MJ_CLEANUP</strong> </a>ファイル オブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549845" data-raw-source="[&lt;strong&gt;MRxCloseSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549845)"><strong>MRxCloseSrvOpen</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが SRV_OPEN 構造体を閉じることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549847" data-raw-source="[&lt;strong&gt;MRxCollapseOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549847)"><strong>MRxCollapseOpen</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが既存の SRV_OPEN に開いているファイル システムの要求を折りたたむことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549850" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549850)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター バッファリング状態の変更要求が完了したことを通知するには、このルーチンを呼び出します。 たとえば、SMB リダイレクターは、oplock 解除の応答を送信するか、ファイルが不要になった使用されている場合は、oplock のハンドルを閉じること、このルーチンを使用します。 サーバーにフラッシュする必要があるバイト範囲ロックは、ネットワークのミニ リダイレクターでに渡される、 <strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT 構造体のメンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549856" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549856)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクターが新しいバッファリング状態の変更を計算することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549862" data-raw-source="[&lt;strong&gt;MRxCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549862)"><strong>MRxCreate</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトを作成することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff548630" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548630)"> <strong>irp_mj_create 用</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549864" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549864)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS では、要求ネットワークのミニ リダイレクターが SRV_CALL 構造を作成し、サーバーとの接続を確立するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549869" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549869)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが V_NET_ROOT 構造を作成することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549871" data-raw-source="[&lt;strong&gt;MRxDeallocateForFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549871)"><strong>MRxDeallocateForFcb</strong></a></td>
<td align="left"><p>RDBSS は、FCB の割り当てを解除するネットワークのミニ リダイレクターを要求するには、このルーチンを呼び出します。 この呼び出しでは、ファイル システム オブジェクトを閉じる要求に応答します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549872" data-raw-source="[&lt;strong&gt;MRxDeallocateForFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549872)"><strong>MRxDeallocateForFobx</strong></a></td>
<td align="left"><p>RDBSS は、FOBX 構造体の割り当てを解除するネットワークのミニ リダイレクターを要求するには、このルーチンを呼び出します。 この呼び出しでは、ファイル システム オブジェクトを閉じる要求に応答します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549876" data-raw-source="[&lt;strong&gt;MRxDevFcbXXXControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549876)"><strong>MRxDevFcbXXXControlFile</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターにデバイス FCB のコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff548649" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548649)"> <strong>IRP_MJ_DEVICE_CONTROL</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff548670" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548670)"> <strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>、または<a href="https://msdn.microsoft.com/library/windows/hardware/ff549241" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549241)"> <strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong> </a> FCB のデバイスにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549878" data-raw-source="[&lt;strong&gt;MRxExtendForCache&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549878)"><strong>MRxExtendForCache</strong></a></td>
<td align="left"><p>RDBSS では、ファイルは、キャッシュ マネージャーによってキャッシュされているときに、ネットワークのミニ リダイレクターがファイルを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549879" data-raw-source="[&lt;strong&gt;MRxExtendForNonCache&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549879)"><strong>MRxExtendForNonCache</strong></a></td>
<td align="left"><p>RDBSS では、キャッシュ マネージャーによって、ファイルがキャッシュされていないときに、ネットワークのミニ リダイレクターがファイルを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550649" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550649)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが指定したパス名から、NET_ROOT の名を抽出することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550653" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550653)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが NET_ROOT オブジェクトをファイナライズすることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550656" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550656)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクター、ファイナライズ SRV_CALL 構造体がサーバーとの接続を確立するために使用されることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550663" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550663)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが V_NET_ROOT オブジェクトをファイナライズすることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550669" data-raw-source="[&lt;strong&gt;MRxFlush&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550669)"><strong>MRxFlush</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトをフラッシュすることを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549235" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549235)"> <strong>IRP_MJ_FLUSH_BUFFERS</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550677" data-raw-source="[&lt;strong&gt;MRxForceClosed&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550677)"><strong>MRxForceClosed</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが終了を強制することを要求するには、このルーチンを呼び出します。 このルーチンは、SRV_OPEN 構造体の状態は不良または SRV_OPEN 構造がクローズとしてマークされるときに呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550687" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550687)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが複数のセッションを処理するために使用できる接続の接続 ID を返すことを要求するには、このルーチンを呼び出します。 接続 Id は、ネットワークのミニ リダイレクターでサポートされる場合、返される接続 ID は、名前のテーブルに格納されている接続の構造に追加されます。 接続 ID のバイト単位の比較は、指定した名前のネットワーク名のテーブルを検索する際にで blob し、RDBSS が接続 ID を非透過 blob と見なします。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550691" data-raw-source="[&lt;strong&gt;MRxIsLockRealizable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550691)"><strong>MRxIsLockRealizable</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが特定 NET_ROOT 構造でバイト範囲ロックはサポートされているかどうかを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550696" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550696)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、パスが有効なディレクトリを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550703" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550703)"><strong>MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、ファイル オブジェクトの排他ロックを開くことを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549251" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549251)"> <strong>IRP_MJ_LOCK_CONTROL</strong> </a> IRP_MN_LOCK のコードを少しでいつ<strong>IrpSp -&gt;フラグ</strong>SL_ がEXCLUSIVE_LOCK ビットが設定されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550709" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550709)"><strong>MRxLowIOSubmit[LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターにファイル システムのコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff548670" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548670)"> <strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550715" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550715)"><strong>MRxLowIOSubmit[LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに I/O システムのコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff548649" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548649)"> <strong>IRP_MJ_DEVICE_CONTROL</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff549241" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549241)"> <strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550721" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550721)"><strong>MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS は、ディレクトリ変更通知操作のネットワークのミニ リダイレクターに要求を発行するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff548658" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548658)"> <strong>IRP_MJ_DIRECTORY_CONTROL</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550724" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550724)"><strong>MRxLowIOSubmit[LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに読み取り要求を発行するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549327" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549327)"> <strong>IRP_MJ_READ</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550734" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550734)"><strong>MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク リダイレクターが、ファイル オブジェクトの共有ロックを開くことを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549251" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549251)"> <strong>IRP_MJ_LOCK_CONTROL</strong> </a> IRP_MN_LOCK のコードを少しでいつ<strong>IrpSp -&gt;フラグ</strong>SL_ がEXCLUSIVE_LOCK ビットが設定されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550740" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550740)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが 1 つのファイル オブジェクトのロックを削除することを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_SINGLE の小さなコードを受信したときにこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550745" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550745)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、ファイル オブジェクトに保持されている複数のロックを削除することを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_ALL または IRP_MN_UNLOCK_ALL_BY_KEY の小さなコードを受信したときにこの呼び出しを発行します。 範囲は、ロックを解除するがで指定された、 <strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT のメンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550746" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550746)"><strong>MRxLowIOSubmit[LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに書き込み要求を発行するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549427" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549427)"> <strong>IRP_MJ_WRITE</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550750" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550750)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクター preparse 名をする機会を提供するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550755" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550755)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS は、ファイル ディレクトリのシステム オブジェクトでネットワークのミニ リダイレクター クエリ情報を要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550759" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550759)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549279" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549279)"> <strong>IRP_MJ_QUERY_EA</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550770" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550770)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ ファイルの情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549283" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549283)"> <strong>IRP_MJ_QUERY_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550773" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550773)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリのクォータ情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549293" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549293)"> <strong>IRP_MJ_QUERY_QUOTA</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550776" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550776)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ セキュリティ記述子の情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549298" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549298)"> <strong>IRP_MJ_QUERY_SECURITY</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550782" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550782)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリのボリューム情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549318" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549318)"> <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550786" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550786)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターのセットがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549346" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549346)"> <strong>IRP_MJ_SET_EA</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550790" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550790)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトでファイルの情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549366" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549366)"> <strong>IRP_MJ_SET_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550796" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550796)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがクリーンアップでファイル システム オブジェクトでファイルの情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS は、アプリケーションがハンドルを閉じますが、オブジェクトには、ファイルの前に、I/O マネージャーによってが閉じられるときに、クリーンアップ中にこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550800" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550800)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターがファイル システム オブジェクトのクォータ情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549401" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549401)"> <strong>IRP_MJ_SET_QUOTA</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550805" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550805)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトのセキュリティ記述子の情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549407" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549407)"> <strong>IRP_MJ_SET_SECURITY</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550810" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550810)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがボリューム情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://msdn.microsoft.com/library/windows/hardware/ff549415" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549415)"> <strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550817" data-raw-source="[&lt;strong&gt;MRxShouldTryToCollapseThisOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550817)"><strong>MRxShouldTryToCollapseThisOpen</strong></a></td>
<td align="left"><p>RDBSS は、RDBSS がお試しくださいし、既存のファイル システム オブジェクトに、オープンの要求を折りたたむかどうかにネットワークのミニ リダイレクターを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550824" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550824)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>このルーチンが「勝者」ネットワークのミニ リダイレクターに通知する RDBSS によって呼び出されるに設計されたときに複数のリダイレクターで、要求を満たすため。 SRV_CALL 構造を作成し、サーバーとの接続を確立するには、優先ネットワーク ミニリダイレクターが予定です。</p>
<p>RDBSS の現在の実装で、RDBSS 層でネットワーク リダイレクターの競合がないために、各ネットワーク ミニリダイレクターは RDBSS のコピーが。 このルーチンは SRV_CALL 構造を作成するすべての要求後に呼び出されます。</p>
<p>同じ汎用名前付け規則 (UNC) の名前空間を処理するため複数リダイレクターがインストールされると、要求をリダイレクターがリダイレクターが、レジストリで指定された順序に基づいて複数 UNC プロバイダー (MUP) によって選択されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550829" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550829)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターを開始するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550833" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550833)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターを停止するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550839" data-raw-source="[&lt;strong&gt;MRxTruncate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550839)"><strong>MRxTruncate</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトを切り捨てることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550844" data-raw-source="[&lt;strong&gt;MRxZeroExtend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550844)"><strong>MRxZeroExtend</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがクリーンアップ時に 0 で、ファイルの入力ファイルのサイズが、FCB の有効なデータの長さより大きい場合、ファイル システム オブジェクトを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 




