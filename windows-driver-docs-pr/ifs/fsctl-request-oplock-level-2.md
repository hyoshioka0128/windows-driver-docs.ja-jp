---
title: FSCTL_REQUEST_OPLOCK_LEVEL_2 制御コード
description: FSCTL\_要求\_OPLOCK\_レベル\_2 制御コードは、ファイルにレベル2の便宜的ロック (oplock) を要求します。
ms.assetid: 418fbbc7-5dca-4c73-8ea0-d4b4e0a2efff
keywords:
- FSCTL_REQUEST_OPLOCK_LEVEL_2 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_REQUEST_OPLOCK_LEVEL_2
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14c57d7a940a40a391d9ea71a968b256b6b81b2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841256"
---
# <a name="fsctl_request_oplock_level_2-control-code"></a>FSCTL\_要求\_OPLOCK\_レベル\_2 制御コード


**FSCTL\_要求\_OPLOCK\_レベル\_2**制御コードは、ファイルにレベル2の便宜的ロック (oplock) を要求します。

この制御コードを処理するために、ミニフィルターは次のパラメーターを使用して[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)を呼び出します。 ファイルシステムまたはレガシフィルタードライバーは、 [**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)を呼び出します。

便宜的ロックの詳細および**FSCTL\_要求\_OPLOCK\_レベル\_2**コントロールコードについては、Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの不透明な oplock オブジェクトポインターです。

<a href="" id="callbackdata"></a>*データの対*  
[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)のみです。 IRP\_MJ\_ファイル\_システム\_CONTROL FSCTL request のコールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造。 操作の*Fscontrolcode*パラメーターは、FSCTL\_REQUEST\_OPLOCK\_レベル\_2 である必要があります。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)のみです。 Irp\_MJ\_ファイル\_システム\_CONTROL FSCTL 要求の IRP。 操作の*Fscontrolcode*パラメーターは、FSCTL\_REQUEST\_OPLOCK\_レベル\_2 である必要があります。

<a href="" id="opencount"></a>*OpenCount*  
ファイルのロック状態を指定します。 ファイルにバイト範囲ロックがある場合は、このパラメーターに0以外の ULONG 値を設定します。それ以外の場合は0を設定します。

<a name="status-block"></a>ステータス ブロック
------------

Oplock が付与されている場合、 [**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)は、この操作に対して FLT\_preop\_PENDING を返します。 それ以外の場合は、FLT\_PREOP\_COMPLETE が返されます。

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
<td align="left"><p><strong>あります</strong></p></td>
<td align="left"><p>Oplock が付与されました。 これは成功コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>IRP は、FSCTL_REQUEST_OPLOCK_LEVEL_2 操作が完了する前に取り消されました。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>Oplock を許可できませんでした。 これはエラーコードです。</p></td>
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

[**FSCTL\_OPLOCK\_中断\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_中断\_確認**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






