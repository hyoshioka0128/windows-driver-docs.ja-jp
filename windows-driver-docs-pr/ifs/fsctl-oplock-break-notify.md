---
title: FSCTL_OPLOCK_BREAK_NOTIFY 制御コード
description: FSCTL\_OPLOCK\_中断\_通知制御コードでは、呼び出し元のアプリケーションが便宜的ロック (oplock) 中断の完了を待機することを許可します。
ms.assetid: 80fe4e5f-fb6f-4c11-8574-97d7f0e7cc6b
keywords:
- FSCTL_OPLOCK_BREAK_NOTIFY 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_OPLOCK_BREAK_NOTIFY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fc160be23d0c913bcc58f614a611aa6f6df3dde
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841272"
---
# <a name="fsctl_oplock_break_notify-control-code"></a>FSCTL\_OPLOCK\_中断\_通知制御コード


**FSCTL\_OPLOCK\_中断\_通知**制御コードでは、呼び出し元のアプリケーションが便宜的ロック (oplock) 中断の完了を待機することを許可します。

この操作は、呼び出し元のハンドルを開いたときに既に開始されていた oplock の中断に対してのみ有効です。 ハンドルが OPLOCKED\_場合は、ファイル\_完了\_で開かれている必要があります。 この操作は、oplock が現在保持されていて、oplock の中断が開始されていない場合は意味がありません。

この制御コードを処理するために、ミニフィルターは次のパラメーターを使用して[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)を呼び出します。 ファイルシステムまたはレガシフィルタードライバーは、 [**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)を呼び出します。

便宜的ロックの詳細および FSCTL\_OPLOCK の詳細については\_制御コードの**通知\_中断**するには Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの不透明な oplock オブジェクトポインターです。

<a href="" id="callbackdata"></a>*データの対*  
[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)のみです。 IRP\_MJ\_ファイル\_システム\_CONTROL FSCTL request のコールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造。 操作の*Fscontrolcode*パラメーターを FSCTL\_OPLOCK\_中断\_通知にする必要があります。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)のみです。 Irp\_MJ\_ファイル\_システム\_CONTROL FSCTL 要求の IRP。 操作の*Fscontrolcode*パラメーターを FSCTL\_OPLOCK\_中断\_通知にする必要があります。

<a href="" id="opencount"></a>*OpenCount*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

Oplock の中断が実行されている場合、 [**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)は FLT\_preop\_PENDING を返し、oplock の解除が完了すると IRP は完了します。 (この場合、IRP は、正常に完了したか、状態\_取り消された状態で完了\_ます)。それ以外の場合、 **FltOplockFsctrl**は FLT\_preop\_COMPLETE を返します。

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
<td align="left"><p>このハンドルで oplock が保持されていないか、oplock が保持されており、oplock ブレークが開始されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>IRP は、FSCTL_OPLOCK_BREAK_NOTIFY 操作が完了する前に取り消されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>あります</strong></p></td>
<td align="left"><p>Oplock の中断が進行中です。 Oplock の解除が完了すると、IRP は完了します。 IRP は、STATUS_SUCCESS または STATUS_CANCELLED のいずれかを使用して最終的に完了できます。 これは成功コードです。</p></td>
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

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






