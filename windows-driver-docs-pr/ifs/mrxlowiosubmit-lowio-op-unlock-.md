---
title: MRxLowIOSubmit\ LOWIO\_OP\_UNLOCK\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_UNLOCK\ ルーチンは、ネットワークのミニ リダイレクターが 1 つのファイル オブジェクトのロックを削除することを要求する RDBSS によって呼び出されます。
ms.assetid: 2985ae12-965d-4871-b56e-2589898932e1
keywords:
- MRxLowIOSubmit LOWIO_OP_UNLOCK ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_UNLOCK
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4531ef8fc3f0facd273abd1599eecc95d759c354
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580306"
---
# <a name="mrxlowiosubmitlowioopunlock-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]ルーチン


*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]* ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターが、1 つを削除することを要求するにはファイル オブジェクトをロックします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_UNLOCK];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_UNLOCK](
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

*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]* ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>無効な応答は、リモート サーバーから受信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターがで指定された<em>RxContext</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>要求を完了するリモート サーバーへの再接続に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンが実装されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_SHARING_VIOLATION</strong></td>
<td align="left"><p>共有違反が発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_UNSUCCESSFUL</strong></td>
<td align="left"><p>呼び出しに失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

RDBSS 呼び出し*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]* 受信への応答、 [ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md) IRP のコードを少し使用して要求\_MN\_UNLOCK\_1 つ。

呼び出しの前に*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]*、RDBSS、RX では、次のメンバーを変更します\_CONTEXT 構造体が、が指す*RxContext*パラメーター。

**LowIoContext.Operation** LOWIO にメンバーが設定されている\_OP\_ロックを解除します。

**LowIoContext.ResourceThreadId**メンバー RDBSS で操作を開始したプロセスのスレッドに設定されます。

**LowIoContext.ParamsFor.Locks.ByteOffset**メンバーの値に設定されます**IrpSp -&gt;Parameters.LockControl.ByteOffset.QuadPart**します。

**LowIoContext.ParamsFor.Locks.Key**メンバーの値に設定されます**IrpSp -&gt;Parameters.LockControl.Key**します。

**LowIoContext.ParamsFor.Locks.Length**メンバーの値に設定されます**IrpSp -&gt;Parameters.LockControl.Length.QuadPart**します。

**LowIoContext.Operation** 、RX のメンバー\_CONTEXT 構造体を低の I/O 操作を実行するを指定します。 ネットワークのミニ リダイレクターで同じルーチンを指すため、低い I/O ルーチンのいくつかのことがこの**LowIoContext.Operation**メンバーは、要求は低の I/O 操作を区別するために使用することができます。 たとえば、ファイルのロックに関連するすべての I/O 呼び出しは、ネットワーク ミニリダイレクターで同じ低い I/O ルーチンを呼び出す可能性があり、このルーチンを使用できます、 **LowIoContext.Operation**ロックとを区別し、ロックを解除するにはメンバー要求される演算。

場合、 *MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]* ルーチン完了までに時間がかかることができます、ネットワークのミニ リダイレクター ドライバーが前に、FCB 構造をリリースする必要がありますネットワーク通信を開始しています。 FCB 構造体を呼び出すことによって解放できます[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)します。 中に、 *MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]* ルーチンは、処理中、 **LowIoContext.ResourceThreadId** RXのメンバー\_コンテキストを RDBSS で操作を開始したプロセスのスレッドを示すことが保証されます。

**LowIoContext.ResourceThreadId** RX のメンバー\_別のスレッドの代わり FCB 構造体を解放するコンテキストを使用できます。 非同期のルーチンが完了したら、最初のスレッドから取得された FCB 構造体を解放できます。

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


[**MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]**](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]**](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






