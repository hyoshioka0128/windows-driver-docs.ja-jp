---
title: FSCTL_OPLOCK_BREAK_ACKNOWLEDGE 制御コード
description: FSCTL\_OPLOCK\_、ファイルに対する排他 (レベル1、バッチ、またはフィルター) 便宜ロック (oplock) が解除されたことを示す通知に制御コードが応答することを\_ます。
ms.assetid: 067aa36b-fa5b-4bc8-bcec-e221509c0d4d
keywords:
- FSCTL_OPLOCK_BREAK_ACKNOWLEDGE 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_OPLOCK_BREAK_ACKNOWLEDGE
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69b0df959202b57c0aa1120ea35ada011cea5b6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841292"
---
# <a name="fsctl_oplock_break_acknowledge-control-code"></a>FSCTL\_OPLOCK\_制御コードの中断\_確認


**FSCTL\_OPLOCK\_** 、ファイルに対する排他 (レベル1、バッチ、またはフィルター) 便宜ロック (oplock) が解除されたことを示す通知に制御コードが応答することを\_ます。

クライアントアプリケーションは、oplock の解除を確認することを示すためにこの制御コードを送信します。また、oplock がレベル2に違反したレベル1の oplock の場合、レベル2の oplock が必要になります。

この制御コードを処理するために、ミニフィルターは次のパラメーターを使用して[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)を呼び出します。 ファイルシステムまたはレガシフィルタードライバーは、 [**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)を呼び出します。

便宜的ロックおよび**FSCTL\_OPLOCK**の詳細については\_制御コードの\_を確認するには Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの不透明な oplock オブジェクトポインターです。

<a href="" id="callbackdata"></a>*データの対*  
[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)のみです。 IRP\_MJ\_ファイル\_システム\_CONTROL FSCTL request のコールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造。 操作の*Fscontrolcode*パラメーターを FSCTL\_OPLOCK\_て、\_の確認を中断する必要があります。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)のみです。 Irp\_MJ\_ファイル\_システム\_CONTROL FSCTL 要求の IRP。 操作の*Fscontrolcode*パラメーターを FSCTL\_OPLOCK\_て、\_の確認を中断する必要があります。

<a href="" id="opencount"></a>*OpenCount*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

レベル1の oplock がレベル2に分割され、レベル2の oplock が許可されている場合、 [**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)はこの操作に対して FLT\_preop\_PENDING を返します。 それ以外の場合は、FLT\_PREOP\_COMPLETE が返されます。

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
<tr class="odd">
<td align="left"><p><strong>あります</strong></p></td>
<td align="left"><p>Oplock の解除が確認されます。 返されると、 <strong>FSCTL_OPLOCK_BREAK_ACKNOWLEDGE</strong>コントロールコードの送信者はレベル2の OPLOCK を保持します。 これは成功コードです。</p></td>
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

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






