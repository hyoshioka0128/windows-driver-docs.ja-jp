---
title: MRxLowIOSubmit\ LOWIO\_OP\_SHAREDLOCK\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_SHAREDLOCK\ ルーチンはネットワーク リダイレクターが、ファイル オブジェクトの共有ロックを開くことを要求する RDBSS によって呼び出されます。
ms.assetid: 963ec2d1-5e24-4002-a8c9-44faf1515b9f
keywords:
- MRxLowIOSubmit LOWIO_OP_SHAREDLOCK ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_SHAREDLOCK
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8209ec0a30c6bacf12a62fa7b2380e2c2a4ad03e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370116"
---
# <a name="mrxlowiosubmitlowioopsharedlock-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\] routine


*MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]* ルーチンを呼び出して[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)ネットワーク リダイレクターが上の共有ロックを開くことを要求するにはファイル オブジェクト。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_SHAREDLOCK](
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

*MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]* ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>要求を完了するリソースの不足が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_BUFFER_SIZE</strong></td>
<td align="left"><p>要求されたバッファー サイズが大きすぎます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>無効な応答は、リモート サーバーから受信しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターがで指定された<em>RxContext</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>要求を完了するリモート サーバーへの再接続に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンが実装されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_SHARING_VIOLATION</strong></td>
<td align="left"><p>共有違反が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_UNSUCCESSFUL</strong></td>
<td align="left"><p>呼び出しに失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS 呼び出し*MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]* 受信に応答する[ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md) IRP のコードを少し使用して要求\_MN\_場合ロック**IrpSp -&gt;フラグ**が、SL\_排他\_ロック ビットが設定されます。

呼び出しの前に*MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]* 、RDBSS、RX では、次のメンバーを変更します\_によって示されるCONTEXT構造体*RxContext*パラメーター。

**LowIoContext.Operation** LOWIO にメンバーが設定されている\_OP\_SHAREDLOCK します。

**LowIoContext.ResourceThreadId**メンバー RDBSS で操作を開始したプロセスのスレッドに設定されます。

**LowIoContext.ParamsFor.Locks.ByteOffset**メンバーの値に設定されます**IrpSp -&gt;Parameters.LockControl.ByteOffset.QuadPart**します。

**LowIoContext.ParamsFor.Locks.Key**メンバーの値に設定されます**IrpSp -&gt;Parameters.LockControl.Key**します。

**LowIoContext.ParamsFor.Locks.Flags**メンバーの値に設定されます**IrpSp -&gt;フラグ**します。

**LowIoContext.ParamsFor.Locks.Length**メンバーの値に設定されます**IrpSp -&gt;Parameters.LockControl.Length.QuadPart**します。

**LowIoContext.Operation** 、RX のメンバー\_CONTEXT 構造体を低の I/O 操作を実行するを指定します。 ネットワークのミニ リダイレクターで同じルーチンを指すため、低い I/O ルーチンのいくつかのことは、 **LowIoContext.Operation**メンバーは、要求は低の I/O 操作を区別するために使用することができます。 たとえば、ファイルのロックに関連するすべての I/O 呼び出しは、ネットワーク ミニリダイレクターで同じ低い I/O ルーチンを呼び出す可能性があり、このルーチンを使用できます、 **LowIoContext.Operation**ロックとを区別し、ロックを解除するにはメンバー要求される演算。

場合、 *MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]* ルーチン完了までに時間がかかることができます、ネットワークのミニ リダイレクター ドライバーが前に、FCB 構造をリリースする必要がありますネットワーク通信を開始しています。 FCB 構造体を呼び出すことによって解放できます[ **RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)します。 中に、 *MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]* ルーチンは、処理中、 **LowIoContext.ResourceThreadId** RX のメンバー\_コンテキスト RDBSS で操作を開始したプロセスのスレッドを示すことが保証されます。

**LowIoContext.ResourceThreadId** 、RX のメンバー\_CONTEXT 構造体を使用して、別のスレッドの代わり FCB 構造体を解放できます。 非同期のルーチンが完了したら、最初のスレッドから取得された FCB 構造体を解放できます。

<a name="requirements"></a>要件
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

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]** ](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






