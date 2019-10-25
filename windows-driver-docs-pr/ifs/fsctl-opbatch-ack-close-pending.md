---
title: FSCTL_OPBATCH_ACK_CLOSE_PENDING 制御コード
description: FSCTL\_OPBATCH\_ACK\_閉じる\_保留中のコントロールコードは、ファイルに対する排他 (レベル1、バッチ、またはフィルター) 便宜ロック (oplock) が解除されたという通知に応答します。
ms.assetid: 310cd778-5a1c-46e2-8c05-127fc754ecfe
keywords:
- FSCTL_OPBATCH_ACK_CLOSE_PENDING 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_OPBATCH_ACK_CLOSE_PENDING
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d21a7b4a2787947dee0d269e7f8cdd572d17f67a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841277"
---
# <a name="fsctl_opbatch_ack_close_pending-control-code"></a>FSCTL\_OPBATCH\_ACK\_終了\_保留中の制御コード


**FSCTL\_OPBATCH\_ACK\_閉じる\_保留中**のコントロールコードは、ファイルに対する排他 (レベル1、バッチ、またはフィルター) 便宜ロック (oplock) が解除されたという通知に応答します。 クライアントアプリケーションは、oplock の解除を確認し、ファイルハンドルを閉じようとしていることを示すために、この制御コードを送信します。

バッチまたはフィルター oplock 解除の場合、呼び出し元は、このコントロールコードを送信した後にファイルハンドルを閉じる必要があります。 それ以外の場合は、ファイルハンドルが閉じられるのを待機している間、システムによってブロックされます。

この制御コードは、レベル1の oplock で使用するためのものではありません。 それにもかかわらず、レベル1の oplock が解除されると、システムはこの制御コードを中断の完全な受信確認として扱い、呼び出し元はファイルハンドルを閉じる必要がありません。

この制御コードはほとんど使用されません。 クライアントアプリケーションにファイルの oplock 解除が通知され、ファイルのハンドルが閉じられると、ファイルハンドルは oplock ブレークの完全な確認として扱われます。 このため、この制御コードを送信する必要はありません。

この制御コードを処理するために、ミニフィルターは次のパラメーターを使用して[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)を呼び出します。 ファイルシステムまたはレガシフィルタードライバーは、 [**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)を呼び出します。

便宜的ロックおよび FSCTL\_OPBATCH\_ACK の詳細については\_保留中の制御コードを閉じる\_については、Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの不透明な oplock オブジェクトポインターです。

<a href="" id="callbackdata"></a>*データの対*  
[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)のみです。 IRP\_MJ\_ファイル\_システム\_CONTROL FSCTL request のコールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造。 操作の*Fscontrolcode*パラメーターを FSCTL\_opbatch\_ACK\_CLOSE\_PENDING を閉じる必要があります。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)のみです。 Irp\_MJ\_ファイル\_システム\_CONTROL FSCTL 要求の IRP。 操作の*Fscontrolcode*パラメーターを FSCTL\_opbatch\_ACK\_CLOSE\_PENDING を閉じる必要があります。

<a href="" id="opencount"></a>*OpenCount*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)は、この操作の FLT\_preop\_COMPLETE を常に返します。

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)は、この操作に対して次のいずれかの NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>このハンドルによって保持されている oplock が壊れています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>このハンドルで oplock が保持されていないか、または oplock ブレークが現在実行中ではありません。 これはエラーコードです。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**IRP\_MJ\_ファイルの FLT\_パラメーター\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL\_OPLOCK\_中断\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_中断\_確認**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






