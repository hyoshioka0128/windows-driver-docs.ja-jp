---
title: FSCTL_OPLOCK_BREAK_ACKNOWLEDGE 制御コード
description: FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE 制御コードは通知に応答する (レベル 1、バッチ、またはフィルター)、排他ファイルの便宜的ロック (oplock) が切断されました。
ms.assetid: 067aa36b-fa5b-4bc8-bcec-e221509c0d4d
keywords:
- FSCTL_OPLOCK_BREAK_ACKNOWLEDGE 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: e20b83612e9aeb556ff383e48f8614e6036265d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572955"
---
# <a name="fsctloplockbreakacknowledge-control-code"></a>FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE 制御コード


**FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE**制御コードは通知に応答する (レベル 1、バッチ、またはフィルター)、排他ファイルの便宜的ロック (oplock) が切断されました。

クライアント アプリケーションは、oplock が受信確認し、oplock がレベル 2 の中断されたレベル 1 の oplock の場合は、レベル 2 oplock をしますが、指定するには、この制御コードを送信します。

ミニフィルターを呼び出し、この制御コードを処理する[ **FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)次のパラメーターを使用します。 ファイル システムまたはレガシ フィルター ドライバーを呼び出す[ **FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)します。

便宜的ロックについて、バージョン情報の詳細については、 **FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE**制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの oplock の不透明なオブジェクトのポインター。

<a href="" id="callbackdata"></a>*ここ*  
[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)のみです。 コールバック データ ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) IRP の構造\_MJ\_ファイル\_システム\_コントロール FSCTL要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPLOCK\_中断\_確認します。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)のみです。 IRP の IRP\_MJ\_ファイル\_システム\_コントロール FSCTL 要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPLOCK\_中断\_確認します。

<a href="" id="opencount"></a>*OpenCount*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)返します FLT\_PREOP\_レベル 1 oplock がレベル 2 の切断され、レベル 2 oplock が許可されている場合、この操作を保留します。 FLT を返しますそれ以外の場合、\_PREOP\_完了します。

[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)この操作は次の NTSTATUS の値を返します。

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
<tr class="odd">
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>Oplock を確認します。 戻り時に、送信者、 <strong>FSCTL_OPLOCK_BREAK_ACKNOWLEDGE</strong>制御コードは、レベル 2 oplock を保持します。 これは、成功コードです。</p></td>
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


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FLT\_IRP のパラメーター\_MJ\_ファイル\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff543398)

[**FSCTL\_OPBATCH\_ACK\_CLOSE\_PENDING**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL\_OPLOCK\_BREAK\_ACK\_NO\_2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






