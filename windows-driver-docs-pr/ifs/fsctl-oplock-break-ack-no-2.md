---
title: FSCTL_OPLOCK_BREAK_ACK_NO_2 制御コード
description: FSCTL\_OPLOCK\_中断\_ACK\_いいえ\_2 の制御コードは通知に応答する (レベル 1、バッチ、またはフィルター)、排他ファイルの便宜的ロック (oplock) が切断されました。
ms.assetid: f76c98ba-e0bf-4b86-bda4-92f233ea5839
keywords:
- FSCTL_OPLOCK_BREAK_ACK_NO_2 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 585b9e40204b95ed87ec882ec712cb5ee0fa3038
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380099"
---
# <a name="fsctloplockbreakackno2-control-code"></a>FSCTL\_OPLOCK\_中断\_ACK\_いいえ\_2 制御コード


**FSCTL\_OPLOCK\_中断\_ACK\_いいえ\_2**制御コードは通知に応答する (レベル 1、バッチ、またはフィルター)、排他便宜的ロック (oplock)ファイルには切断されました。

クライアント アプリケーションでは、このコントロールのコードを oplock が受信確認し、oplock がレベル 2 の中断されたレベル 1 の oplock の場合は、そのたくないレベル 2 oplock を示すために送信します。

ミニフィルターを呼び出し、この制御コードを処理する[ **FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)次のパラメーターを使用します。 ファイル システムまたはレガシ フィルター ドライバーを呼び出す[ **FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)します。

便宜的ロックおよび FSCTL についての詳細については\_OPLOCK\_中断\_ACK\_いいえ\_2 制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの oplock の不透明なオブジェクトのポインター。

<a href="" id="callbackdata"></a>*ここ*  
[**FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)のみです。 コールバック データ ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) IRP の構造\_MJ\_ファイル\_システム\_コントロール FSCTL要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPLOCK\_中断\_ACK\_いいえ\_2。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)のみです。 IRP の IRP\_MJ\_ファイル\_システム\_コントロール FSCTL 要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPLOCK\_中断\_ACK\_いいえ\_2。

<a href="" id="opencount"></a>*OpenCount*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl) FLT は常に返します\_PREOP\_この操作を完了します。

[**FsRtlOplockFsctrl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)この操作は次の NTSTATUS の値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>Oplock を確認します。 残りの各 oplock は保持されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>このハンドルによって保持された oplock がないか、oplock は現在進行中のありません。 これは、エラー コードです。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FLT\_IRP のパラメーター\_MJ\_ファイル\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL\_OPBATCH\_ACK\_CLOSE\_PENDING**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






