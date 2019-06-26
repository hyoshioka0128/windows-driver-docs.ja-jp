---
title: MRxLowIOSubmit\ LOWIO\_OP\_IOCTL\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_IOCTL\ ルーチンは、ネットワークのミニ リダイレクターに I/O システムのコントロール要求を発行する RDBSS によって呼び出されます。
ms.assetid: b416e2b4-6024-45ec-adf5-90743d417ad5
keywords:
- MRxLowIOSubmit LOWIO_OP_IOCTL ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_IOCTL
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70da29cda27ab0d4387c6bf5b0b273c0dcc8e032
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363510"
---
# <a name="mrxlowiosubmitlowioopioctl-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]ルーチン


*MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]* ルーチンを呼び出して[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)ネットワークに、I/O システムのコントロール要求を発行するにはミニ リダイレクター。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_IOCTL];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_IOCTL](
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]* ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>要求を完了するリソースの不足が発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>無効なデバイス、要求が指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターがで指定された<em>RxContext</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンが実装されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>指定された IOCTL はネットワーク ミニリダイレクターではサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS 呼び出し*MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]* 受信に応答する[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)要求します。

呼び出しの前に*MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]* 、RDBSS、RX では、次のメンバーを変更します\_CONTEXT 構造体が、が指す*RxContext*パラメーター。

**LowIoContext.Operation** LOWIO にメンバーが設定されている\_OP\_IOCTL します。

**LowIoContext.ResourceThreadId**メンバー RDBSS で操作を開始したプロセスのスレッドに設定されます。

**LowIoContext.ParamsFor.IoCtl.IoControlCode**メンバー IOCTL 制御コードに設定されます。

**LowIoContext.ParamsFor.IoCtl.pInputBuffer**メンバーは、入力バッファーに設定します。

**LowIoContext.ParamsFor.IoCtl.InputBufferLength**メンバーは、入力バッファーの長さに設定します。

**LowIoContext.ParamsFor.IoCtl.pOutputBuffer**メンバーは、出力バッファーに設定されます。

**LowIoContext.ParamsFor.IoCtl.OutputBufferLength**メンバーは、出力バッファーの長さに設定します。

中に、 *MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]* ルーチンは、処理中、 **LowIoContext.ResourceThreadId** RXのメンバー\_コンテキストを RDBSS で操作を開始したプロセスのスレッドを示すことが保証されます。 **LowIoContext.ResourceThreadId** RX のメンバー\_コンテキストは、別のスレッドの代わりの入力のリソースを解放するために使用できます。 非同期のルーチンが完了したら、最初のスレッドから取得された入力のリソースを解放できます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]** ](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]** ](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]** ](mrxlowiosubmit-lowio-op-write-.md)

 

 






