---
title: FSCTL_REQUEST_FILTER_OPLOCK 制御コード
description: FSCTL\_要求\_フィルター\_OPLOCK 制御コードは、フィルターの便宜的ロック (oplock) ファイルを要求します。
ms.assetid: 9d6b2773-db87-492c-8fe9-f5fd4ef2eb7b
keywords:
- FSCTL_REQUEST_FILTER_OPLOCK 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_REQUEST_FILTER_OPLOCK
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1960a96da77404eae19df9edb45d0f6b9875919
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372690"
---
# <a name="fsctlrequestfilteroplock-control-code"></a>FSCTL\_要求\_フィルター\_OPLOCK 制御コード


**FSCTL\_要求\_フィルター\_OPLOCK**制御コードは、フィルターの便宜的ロック (oplock) ファイルを要求します。

ミニフィルターを呼び出し、この制御コードを処理する[ **FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)次のパラメーターを使用します。 ファイル システムまたはレガシ フィルター ドライバーを呼び出す[ **FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)します。

便宜的ロックについて、バージョン情報の詳細については、 **FSCTL\_要求\_フィルター\_OPLOCK**制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの oplock の不透明なオブジェクトのポインター。

<a href="" id="callbackdata"></a>*ここ*  
[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)のみです。 コールバック データ ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) IRP の構造\_MJ\_ファイル\_システム\_コントロール FSCTL要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_要求\_フィルター\_OPLOCK します。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)のみです。 IRP の IRP\_MJ\_ファイル\_システム\_コントロール FSCTL 要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_要求\_フィルター\_OPLOCK します。

<a href="" id="opencount"></a>*OpenCount*  
ユーザーの数は、ファイルを処理します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)返します FLT\_PREOP\_oplock が付与された場合は、この操作を保留します。 FLT を返しますそれ以外の場合、\_PREOP\_完了します。

[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)この操作は次の NTSTATUS の値を返します。

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
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>Oplock が与えられました。 これは、成功コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>FSCTL_REQUEST_BATCH_OPLOCK 操作が完了する前に、IRP が取り消されました。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>Oplock を取得できませんでした。 これは、エラー コードです。</p></td>
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

[**FSCTL\_OPLOCK\_中断\_ACKNOWLEDGE**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_中断\_通知**](fsctl-oplock-break-notify.md)

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






