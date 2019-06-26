---
title: カーネル ネットワーク ミニリダイレクターによって実装されるルーチン
description: カーネル ネットワーク ミニリダイレクターによって実装されるルーチン
ms.assetid: bd1a8989-100d-4b7b-9a61-521af6433b00
keywords:
- ミニ-リダイレクター WDK、ルーチンの実装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7010147ea7809654a99586c8913e902421a2b34d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371930"
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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkfcb_calldown" data-raw-source="[&lt;strong&gt;MRxAreFilesAliased&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkfcb_calldown)"><strong>MRxAreFilesAliased</strong></a></td>
<td align="left"><p>RDBSS では、2 つのファイル制御ブロック (FCB) 構造体が同じファイルを表す場合は、ネットワークのミニ リダイレクターを照会するには、このルーチンを呼び出します。 別の名前 (MS-DOS の短い名前と例については、長い名前) がある同じにするファイルの 2 つの処理時にこのルーチン RDBSS 呼び出しが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85)" data-raw-source="[&lt;strong&gt;MRxCleanupFobx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))"><strong>MRxCleanupFobx</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトの拡張機能の構造を閉じることを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-cleanup)"> <strong>IRP_MJ_CLEANUP</strong> </a>ファイル オブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown" data-raw-source="[&lt;strong&gt;MRxCloseSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown)"><strong>MRxCloseSrvOpen</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが SRV_OPEN 構造体を閉じることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen" data-raw-source="[&lt;strong&gt;MRxCollapseOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen)"><strong>MRxCollapseOpen</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが既存の SRV_OPEN に開いているファイル システムの要求を折りたたむことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_change_buffering_state_calldown" data-raw-source="[&lt;strong&gt;MRxCompleteBufferingStateChangeRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_change_buffering_state_calldown)"><strong>MRxCompleteBufferingStateChangeRequest</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター バッファリング状態の変更要求が完了したことを通知するには、このルーチンを呼び出します。 たとえば、SMB リダイレクターは、oplock 解除の応答を送信するか、ファイルが不要になった使用されている場合は、oplock のハンドルを閉じること、このルーチンを使用します。 サーバーにフラッシュする必要があるバイト範囲ロックは、ネットワークのミニ リダイレクターでに渡される、 <strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT 構造体のメンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_compute_new_buffering_state" data-raw-source="[&lt;strong&gt;MRxComputeNewBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_compute_new_buffering_state)"><strong>MRxComputeNewBufferingState</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクターが新しいバッファリング状態の変更を計算することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate" data-raw-source="[&lt;strong&gt;MRxCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)"><strong>MRxCreate</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトを作成することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)"> <strong>irp_mj_create 用</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_srvcall)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS では、要求ネットワークのミニ リダイレクターが SRV_CALL 構造を作成し、サーバーとの接続を確立するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_create_v_net_root)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが V_NET_ROOT 構造を作成することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fcb" data-raw-source="[&lt;strong&gt;MRxDeallocateForFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fcb)"><strong>MRxDeallocateForFcb</strong></a></td>
<td align="left"><p>RDBSS は、FCB の割り当てを解除するネットワークのミニ リダイレクターを要求するには、このルーチンを呼び出します。 この呼び出しでは、ファイル システム オブジェクトを閉じる要求に応答します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fobx" data-raw-source="[&lt;strong&gt;MRxDeallocateForFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fobx)"><strong>MRxDeallocateForFobx</strong></a></td>
<td align="left"><p>RDBSS は、FOBX 構造体の割り当てを解除するネットワークのミニ リダイレクターを要求するには、このルーチンを呼び出します。 この呼び出しでは、ファイル システム オブジェクトを閉じる要求に応答します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile" data-raw-source="[&lt;strong&gt;MRxDevFcbXXXControlFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile)"><strong>MRxDevFcbXXXControlFile</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターにデバイス FCB のコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)"> <strong>IRP_MJ_DEVICE_CONTROL</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)"> <strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control)"> <strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong> </a> FCB のデバイスにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extendfile_calldown" data-raw-source="[&lt;strong&gt;MRxExtendForCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extendfile_calldown)"><strong>MRxExtendForCache</strong></a></td>
<td align="left"><p>RDBSS では、ファイルは、キャッシュ マネージャーによってキャッシュされているときに、ネットワークのミニ リダイレクターがファイルを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache" data-raw-source="[&lt;strong&gt;MRxExtendForNonCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache)"><strong>MRxExtendForNonCache</strong></a></td>
<td align="left"><p>RDBSS では、キャッシュ マネージャーによって、ファイルがキャッシュされていないときに、ネットワークのミニ リダイレクターがファイルを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extract_netroot_name" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extract_netroot_name)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが指定したパス名から、NET_ROOT の名を抽出することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_net_root_calldown)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが NET_ROOT オブジェクトをファイナライズすることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_srvcall_calldown)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクター、ファイナライズ SRV_CALL 構造体がサーバーとの接続を確立するために使用されることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_finalize_v_net_root_calldown)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが V_NET_ROOT オブジェクトをファイナライズすることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush" data-raw-source="[&lt;strong&gt;MRxFlush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush)"><strong>MRxFlush</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトをフラッシュすることを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-flush-buffers" data-raw-source="[&lt;strong&gt;IRP_MJ_FLUSH_BUFFERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-flush-buffers)"> <strong>IRP_MJ_FLUSH_BUFFERS</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_forceclosed_calldown" data-raw-source="[&lt;strong&gt;MRxForceClosed&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_forceclosed_calldown)"><strong>MRxForceClosed</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが終了を強制することを要求するには、このルーチンを呼び出します。 このルーチンは、SRV_OPEN 構造体の状態は不良または SRV_OPEN 構造がクローズとしてマークされるときに呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_get_connection_id" data-raw-source="[&lt;strong&gt;MRxGetConnectionId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_get_connection_id)"><strong>MRxGetConnectionId</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが複数のセッションを処理するために使用できる接続の接続 ID を返すことを要求するには、このルーチンを呼び出します。 接続 Id は、ネットワークのミニ リダイレクターでサポートされる場合、返される接続 ID は、名前のテーブルに格納されている接続の構造に追加されます。 接続 ID のバイト単位の比較は、指定した名前のネットワーク名のテーブルを検索する際にで blob し、RDBSS が接続 ID を非透過 blob と見なします。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_is_lock_realizable" data-raw-source="[&lt;strong&gt;MRxIsLockRealizable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_is_lock_realizable)"><strong>MRxIsLockRealizable</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが特定 NET_ROOT 構造でバイト範囲ロックはサポートされているかどうかを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkdir_calldown" data-raw-source="[&lt;strong&gt;MRxIsValidDirectory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkdir_calldown)"><strong>MRxIsValidDirectory</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、パスが有効なディレクトリを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-exclusivelock-)"><strong>MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、ファイル オブジェクトの排他ロックを開くことを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)"> <strong>IRP_MJ_LOCK_CONTROL</strong> </a> IRP_MN_LOCK のコードを少しでいつ<strong>IrpSp -&gt;フラグ</strong>SL_ がEXCLUSIVE_LOCK ビットが設定されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_FSCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-fsctl-)"><strong>MRxLowIOSubmit[LOWIO_OP_FSCTL]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターにファイル システムのコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control" data-raw-source="[&lt;strong&gt;IRP_MJ_FILE_SYSTEM_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)"> <strong>IRP_MJ_FILE_SYSTEM_CONTROL</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_IOCTL]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-ioctl-)"><strong>MRxLowIOSubmit[LOWIO_OP_IOCTL]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに I/O システムのコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)"> <strong>IRP_MJ_DEVICE_CONTROL</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-internal-device-control)"> <strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-notify-change-directory-)"><strong>MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY]</strong></a></td>
<td align="left"><p>RDBSS は、ディレクトリ変更通知操作のネットワークのミニ リダイレクターに要求を発行するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DIRECTORY_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)"> <strong>IRP_MJ_DIRECTORY_CONTROL</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_READ]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-read-)"><strong>MRxLowIOSubmit[LOWIO_OP_READ]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに読み取り要求を発行するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-read)"> <strong>IRP_MJ_READ</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-sharedlock-)"><strong>MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK]</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク リダイレクターが、ファイル オブジェクトの共有ロックを開くことを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control" data-raw-source="[&lt;strong&gt;IRP_MJ_LOCK_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)"> <strong>IRP_MJ_LOCK_CONTROL</strong> </a> IRP_MN_LOCK のコードを少しでいつ<strong>IrpSp -&gt;フラグ</strong>SL_ がEXCLUSIVE_LOCK ビットが設定されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが 1 つのファイル オブジェクトのロックを削除することを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_SINGLE の小さなコードを受信したときにこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-unlock-multiple-)"><strong>MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが、ファイル オブジェクトに保持されている複数のロックを削除することを要求するには、このルーチンを呼び出します。 RDBSS、IRP_MJ_LOCK_CONTROL IRP_MN_UNLOCK_ALL または IRP_MN_UNLOCK_ALL_BY_KEY の小さなコードを受信したときにこの呼び出しを発行します。 範囲は、ロックを解除するがで指定された、 <strong>LowIoContext.ParamsFor.Locks.LockList</strong> RX_CONTEXT のメンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-" data-raw-source="[&lt;strong&gt;MRxLowIOSubmit[LOWIO_OP_WRITE]&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxlowiosubmit-lowio-op-write-)"><strong>MRxLowIOSubmit[LOWIO_OP_WRITE]</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターに書き込み要求を発行するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)"> <strong>IRP_MJ_WRITE</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_preparse_name" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_preparse_name)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクター preparse 名をする機会を提供するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerydirectory" data-raw-source="[&lt;strong&gt;MRxQueryDirectory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerydirectory)"><strong>MRxQueryDirectory</strong></a></td>
<td align="left"><p>RDBSS は、ファイル ディレクトリのシステム オブジェクトでネットワークのミニ リダイレクター クエリ情報を要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryeainfo" data-raw-source="[&lt;strong&gt;MRxQueryEaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryeainfo)"><strong>MRxQueryEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_EA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)"> <strong>IRP_MJ_QUERY_EA</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo" data-raw-source="[&lt;strong&gt;MRxQueryFileInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo)"><strong>MRxQueryFileInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ ファイルの情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-information)"> <strong>IRP_MJ_QUERY_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryquotainfo" data-raw-source="[&lt;strong&gt;MRxQueryQuotaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryquotainfo)"><strong>MRxQueryQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリのクォータ情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_QUOTA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)"> <strong>IRP_MJ_QUERY_QUOTA</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerysdinfo" data-raw-source="[&lt;strong&gt;MRxQuerySdInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxquerysdinfo)"><strong>MRxQuerySdInfo</strong></a></td>
<td align="left"><p>RDBSS は、ファイル システム オブジェクトでネットワーク ミニリダイレクター クエリ セキュリティ記述子の情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_SECURITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)"> <strong>IRP_MJ_QUERY_SECURITY</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryvolumeinfo" data-raw-source="[&lt;strong&gt;MRxQueryVolumeInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryvolumeinfo)"><strong>MRxQueryVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニリダイレクター クエリのボリューム情報を要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_QUERY_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)"> <strong>IRP_MJ_QUERY_VOLUME_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxseteainfo" data-raw-source="[&lt;strong&gt;MRxSetEaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxseteainfo)"><strong>MRxSetEaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターのセットがファイル システム オブジェクトの属性情報を拡張することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_EA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)"> <strong>IRP_MJ_SET_EA</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfo" data-raw-source="[&lt;strong&gt;MRxSetFileInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfo)"><strong>MRxSetFileInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトでファイルの情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-information)"> <strong>IRP_MJ_SET_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup" data-raw-source="[&lt;strong&gt;MRxSetFileInfoAtCleanup&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetfileinfoatcleanup)"><strong>MRxSetFileInfoAtCleanup</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがクリーンアップでファイル システム オブジェクトでファイルの情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS は、アプリケーションがハンドルを閉じますが、オブジェクトには、ファイルの前に、I/O マネージャーによってが閉じられるときに、クリーンアップ中にこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetquotainfo" data-raw-source="[&lt;strong&gt;MRxSetQuotaInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetquotainfo)"><strong>MRxSetQuotaInfo</strong></a></td>
<td align="left"><p>RDBSS は、ネットワーク ミニ リダイレクターがファイル システム オブジェクトのクォータ情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_QUOTA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)"> <strong>IRP_MJ_SET_QUOTA</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetsdinfo" data-raw-source="[&lt;strong&gt;MRxSetSdInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetsdinfo)"><strong>MRxSetSdInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトのセキュリティ記述子の情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_SECURITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)"> <strong>IRP_MJ_SET_SECURITY</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetvolumeinfo" data-raw-source="[&lt;strong&gt;MRxSetVolumeInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxsetvolumeinfo)"><strong>MRxSetVolumeInfo</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがボリューム情報を設定することを要求するには、このルーチンを呼び出します。 RDBSS が応答を受信するには、この呼び出しを発行する<a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information" data-raw-source="[&lt;strong&gt;IRP_MJ_SET_VOLUME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)"> <strong>IRP_MJ_SET_VOLUME_INFORMATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen" data-raw-source="[&lt;strong&gt;MRxShouldTryToCollapseThisOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen)"><strong>MRxShouldTryToCollapseThisOpen</strong></a></td>
<td align="left"><p>RDBSS は、RDBSS がお試しくださいし、既存のファイル システム オブジェクトに、オープンの要求を折りたたむかどうかにネットワークのミニ リダイレクターを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_srvcall_winner_notify)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>このルーチンが「勝者」ネットワークのミニ リダイレクターに通知する RDBSS によって呼び出されるに設計されたときに複数のリダイレクターで、要求を満たすため。 SRV_CALL 構造を作成し、サーバーとの接続を確立するには、優先ネットワーク ミニリダイレクターが予定です。</p>
<p>RDBSS の現在の実装で、RDBSS 層でネットワーク リダイレクターの競合がないために、各ネットワーク ミニリダイレクターは RDBSS のコピーが。 このルーチンは SRV_CALL 構造を作成するすべての要求後に呼び出されます。</p>
<p>同じ汎用名前付け規則 (UNC) の名前空間を処理するため複数リダイレクターがインストールされると、要求をリダイレクターがリダイレクターが、レジストリで指定された順序に基づいて複数 UNC プロバイダー (MUP) によって選択されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターを開始するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターを停止するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate" data-raw-source="[&lt;strong&gt;MRxTruncate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate)"><strong>MRxTruncate</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトを切り捨てることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend" data-raw-source="[&lt;strong&gt;MRxZeroExtend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend)"><strong>MRxZeroExtend</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがクリーンアップ時に 0 で、ファイルの入力ファイルのサイズが、FCB の有効なデータの長さより大きい場合、ファイル システム オブジェクトを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 




