---
title: MRxLowIOSubmit\ LOWIO\_OP\_WRITE\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_WRITE\ ルーチンは、ネットワークのミニ リダイレクターに書き込み要求を発行する RDBSS によって呼び出されます。
ms.assetid: b70838e3-4e80-4ec9-88ba-0f608a1af78e
keywords:
- MRxLowIOSubmit LOWIO_OP_WRITE ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_WRITE
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cd664597f907a03ca874878134fac189bf01f65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324491"
---
# <a name="mrxlowiosubmitlowioopwrite-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]ルーチン


*MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]* ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニリダイレクターに書き込み要求を発行します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_WRITE];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_WRITE](
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

*MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]* ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_FILE_CLOSED</strong></td>
<td align="left"><p>FCB 構造体を取得したが、関連付けられている SRV_OPEN 構造が閉じられました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>要求を完了するリソースの不足が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>無効なデバイス、要求が指定されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターがで指定された<em>RxContext</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンが実装されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>ネットワークのミニ リダイレクターでは、指定された要求がサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS 呼び出し*MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]* 受信に応答する[ **IRP\_MJ\_書き込み** ](irp-mj-write.md)要求。

呼び出しの前に*MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]*、RDBSS、RX では、次のメンバーを変更します\_CONTEXT 構造体が、が指す*RxContext*パラメーター。

**LowIoContext.Operation** LOWIO にメンバーが設定されている\_OP\_を記述します。

**LowIoContext.ResourceThreadId**メンバー RDBSS で操作を開始したプロセスのスレッドに設定されます。

**LowIoContext.ParamsFor.ReadWrite.Key**メンバーの値に設定されます**IrpSp -&gt;Parameters.Read.Key**します。

**ParamsFor.ReadWrite.Flags**メンバーが、LOWIO\_READWRITEFLAG\_ページング\_場合の IO のビットが設定されて**Irp -&gt;フラグ**IRPが\_ページング\_IO ビットにします。

**ParamsFor.ReadWrite.Buffer**メンバー IoWriteAccess のロックされているユーザーのバッファーに設定されます。

**LowIoContext.ParamsFor.ReadWrite.ByteCount**メンバーの値に設定されます**IrpSp -&gt;Parameters.Write.Length**します。

書き込み要求通常によって実装されますネットワーク ミニリダイレクター非同期操作として非常に長い時間がかかるためです。 通常、操作は、リモート サーバーにネットワーク要求を送信するので構成されます。 サーバー上の書き込み要求が完了したときに、応答が取得されます。 これは、ローカルで開始されたキャンセルを処理するためのコンテキストを登録する必要がありますネットワーク ミニリダイレクター操作の例です。

中に、 *MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]* ルーチンは、処理中、 **LowIoContext.ResourceThreadId** RXのメンバー\_コンテキストを RDBSS で操作を開始したプロセスのスレッドを示すことが保証されます。 **LowIoContext.ResourceThreadId**別のスレッドの代わり FCB 構造体を解放するメンバーを使用することができます。 非同期のルーチンが完了したら、最初のスレッドから取得された FCB 構造体を解放できます。 FCB 構造体を呼び出すことによって解放できます[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)します。

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

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






