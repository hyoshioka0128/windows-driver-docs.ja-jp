---
title: MRxLowIOSubmit\ LOWIO\_OP\_UNLOCK\_MULTIPLE\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_UNLOCK\_ネットワーク ミニ リダイレクターが、ファイル オブジェクトに保持されている複数のロックを削除することを要求する RDBSS によって複数のルーチンが呼び出されます。
ms.assetid: 50f7abdf-a3f7-4625-ac54-75e80807d05e
keywords:
- MRxLowIOSubmit LOWIO_OP_UNLOCK_MULTIPLE ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_UNLOCK_MULTIPLE
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 085d3c72ab7fab2eb651a586030431bd363ed202
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324446"
---
# <a name="mrxlowiosubmitlowioopunlockmultiple-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_複数\]ルーチン


*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_複数\]* ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)を要求できるネットワークミニ リダイレクターは、ファイル オブジェクトに保持されている複数のロックを削除します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_UNLOCK_MULTIPLE](
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

*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_複数\]* ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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

 

<a name="remarks"></a>注釈
-------

RDBSS 呼び出し*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_複数\]* 受信への応答、 [ **IRP\_MJ\_ロック\_コントロール**](irp-mj-lock-control.md) IRP のコードを少し使用して要求\_MN\_UNLOCK\_すべてまたは IRP\_MN\_ロックの解除\_すべて\_BY\_キー。

呼び出しの前に*MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_複数\]*、RDBSS、RX では、次のメンバーを変更します\_CONTEXT 構造体によって示される、 *RxContext*パラメーター。

**LowIoContext.Operation** LOWIO にメンバーが設定されている\_OP\_UNLOCK\_複数。

**LowIoContext.ResourceThreadId**メンバー RDBSS で操作を開始したプロセスのスレッドに設定されます。

**LowIoContext.ParamsFor.Locks.LockList** LOWIO の一覧にメンバーが設定されている\_ロック\_リストの要素。 各要素は、ロックを解除する範囲を指定します。

バイト範囲は、ロックを解除するがで指定された、 **LowIoContext.ParamsFor.Locks.LockList** 、RX のメンバー\_CONTEXT 構造体。 LOWIO\_ロック\_リスト構造を次に示します。

``` syntax
typedef struct _LOWIO_LOCK_LIST {
  struct  _LOWIO_LOCK_LIST  *Next;
  ULONG  LockNumber;
  RXVBO  ByteOffset;
  LONGLONG  Length;
  ULONG  Key;
  BOOLEAN  ExclusiveLock;
} LOWIO_LOCK_LIST, *PLOWIO_LOCK_LIST;
```

**LowIoContext.Operation** RX のメンバー\_コンテキストを低の I/O 操作を実行するを指定します。 ネットワークのミニ リダイレクターで同じルーチンを指すため、低い I/O ルーチンのいくつかのことは、 **LowIoContext.Operation**メンバーは、要求は低の I/O 操作を区別するために使用することができます。 たとえば、ファイルのロックに関連するすべての I/O 呼び出しは、ネットワーク ミニリダイレクターで同じ低い I/O ルーチンを呼び出す可能性があり、このルーチンを使用できます、 **LowIoContext.Operation**ロックとを区別し、ロックを解除するにはメンバー要求される演算。

場合、 *MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_複数\]* ルーチン完了までに時間がかかることができます、ネットワークのミニ リダイレクター ドライバーをリリースする必要があります、FCB のネットワーク通信を開始する前に構造体。 FCB 構造体を呼び出すことによって解放できます[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)します。 中に、 *MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_複数\]* ルーチンは、処理中、 **LowIoContext.ResourceThreadId** RX のメンバー\_コンテキスト RDBSS で操作を開始したプロセスのスレッドを示すことが保証されます。

**LowIoContext.ResourceThreadId** RX のメンバー\_別のスレッドの代わり FCB 構造体を解放するコンテキストを使用できます。 非同期のルーチンが完了したら、最初のスレッドから取得された FCB 構造体を解放できます。

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


[**MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]**](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]**](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]**](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\]**](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






