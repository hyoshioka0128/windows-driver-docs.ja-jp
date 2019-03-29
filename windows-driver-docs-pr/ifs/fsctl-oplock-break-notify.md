---
title: FSCTL_OPLOCK_BREAK_NOTIFY 制御コード
description: FSCTL\_OPLOCK\_BREAK\_通知制御コードにより、呼び出し元のアプリケーションの便宜的ロック (oplock) 中断の完了を待ちます。
ms.assetid: 80fe4e5f-fb6f-4c11-8574-97d7f0e7cc6b
keywords:
- FSCTL_OPLOCK_BREAK_NOTIFY 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: c81233d920e7adc86bb1a39fee46bf6bf86ab956
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582634"
---
# <a name="fsctloplockbreaknotify-control-code"></a>FSCTL\_OPLOCK\_中断\_通知制御コード


**FSCTL\_OPLOCK\_BREAK\_通知**制御コードにより、呼び出し元のアプリケーションの便宜的ロック (oplock) 中断の完了を待ちます。

この操作は、呼び出し元のハンドルが開かれたときに既に開始された oplock に対してのみ有効です。 ファイルを使用して、ハンドルが開かれている必要があります\_完了\_場合\_OPLOCKED します。 Oplock が現在保持されているし、oplock が開始されていない場合、この操作は無意味です。

ミニフィルターを呼び出し、この制御コードを処理する[ **FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)次のパラメーターを使用します。 ファイル システムまたはレガシ フィルター ドライバーを呼び出す[ **FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)します。

便宜的ロックについて、バージョン情報の詳細については、 **FSCTL\_OPLOCK\_中断\_通知**制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
ファイルの oplock の不透明なオブジェクトのポインター。

<a href="" id="callbackdata"></a>*ここ*  
[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)のみです。 コールバック データ ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) IRP の構造\_MJ\_ファイル\_システム\_コントロール FSCTL要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPLOCK\_中断\_に通知します。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)のみです。 IRP の IRP\_MJ\_ファイル\_システム\_コントロール FSCTL 要求。 *FsControlCode*操作のパラメーターに FSCTL をする必要があります\_OPLOCK\_中断\_に通知します。

<a href="" id="opencount"></a>*OpenCount*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)返します FLT\_PREOP\_PENDING、oplock が進行中、および、oplock が完了すると、IRP が完了する場合。 (この場合、IRP は、いずれかの状態で完了できる最終的に\_成功または状態\_取り消されました)。それ以外の場合、 **FltOplockFsctrl**返します FLT\_PREOP\_完了します。

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
<td align="left"><p>このハンドルによって保持された oplock がないまたは oplock が保持されているし、oplock が開始されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>FSCTL_OPLOCK_BREAK_NOTIFY 操作が完了する前に、IRP が取り消されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>Oplock が進行中です。 IRP は、oplock の完了時に実行されます。 IRP を STATUS_SUCCESS または STATUS_CANCELLED のいずれかで最終的に完了できます。 これは、成功コードです。</p></td>
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

[**FSCTL\_要求\_バッチ\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_要求\_フィルター\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_要求\_OPLOCK\_レベル\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






