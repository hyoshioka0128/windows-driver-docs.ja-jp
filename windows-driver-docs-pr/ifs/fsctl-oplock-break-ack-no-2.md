---
title: FSCTL_OPLOCK_BREAK_ACK_NO_2 制御コード
description: FSCTL\_OPLOCK\_は、ファイルに対する排他 (レベル1、バッチ、またはフィルター) 便宜ロック (oplock) が解除されたという通知に対して、\_2 の制御コードが応答しなくなったことを中断\_\_ます。
ms.assetid: f76c98ba-e0bf-4b86-bda4-92f233ea5839
keywords:
- FSCTL_OPLOCK_BREAK_ACK_NO_2 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_OPLOCK_BREAK_ACK_NO_2
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d5708eaadd9d44b99ec3af78f485b30dfc5e002
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841274"
---
# <a name="fsctl_oplock_break_ack_no_2-control-code"></a>FSCTL\_OPLOCK\_中断\_ACK\_\_2 制御コードなし


FSCTL\_OPLOCK\_は、ファイルに対する排他 (レベル1、バッチ、またはフィルター) 便宜ロック (oplock) が解除されたという通知に対して、\_2 の制御コードが応答しなくなったことを**中断\_\_** ます。

クライアントアプリケーションは、oplock の解除を確認することを示すためにこの制御コードを送信します。また、oplock がレベル2に違反したレベル1の oplock の場合、レベル2の oplock は必要ありません。

この制御コードを処理するために、ミニフィルターは次のパラメーターを使用して[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)を呼び出します。 ファイルシステムまたはレガシフィルタードライバーは、 [**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)を呼び出します。

便宜的ロックの詳細と、FSCTL\_OPLOCK の詳細については、\_2 の制御コードを使用せずに\_\_ACK を\_中断するには、Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの不透明な oplock オブジェクトポインターです。

<a href="" id="callbackdata"></a>*データの対*  
[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)のみです。 IRP\_MJ\_ファイル\_システム\_CONTROL FSCTL request のコールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造。 操作の*Fscontrolcode*パラメーターを FSCTL\_OPLOCK\_、\_2 ではなく\_\_ACK を中断する必要があります。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)のみです。 Irp\_MJ\_ファイル\_システム\_CONTROL FSCTL 要求の IRP。 操作の*Fscontrolcode*パラメーターを FSCTL\_OPLOCK\_、\_2 ではなく\_\_ACK を中断する必要があります。

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
<td align="left"><p>Oplock の解除が確認されます。 残りの oplock は保持されません。</p></td>
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

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_ファイルの FLT\_パラメーター\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL\_OPBATCH\_ACK\_終了\_保留中**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL\_OPLOCK\_中断\_確認**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






