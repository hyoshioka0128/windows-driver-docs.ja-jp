---
title: MRxLowIOSubmit \ LOWIO\_OP\_EXCLUSIVELOCK \ ルーチン
description: MRxLowIOSubmit \ LOWIO\_OP\_EXCLUSIVELOCK \ ルーチンは RDBSS によって呼び出され、ネットワークミニリダイレクターがファイルオブジェクトの排他ロックを開くことを要求します。
ms.assetid: 7f6613d1-63fb-4505-966d-155dc2b80ffe
keywords:
- MRxLowIOSubmit LOWIO_OP_EXCLUSIVELOCK ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_EXCLUSIVELOCK
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c415a76228751be395b17ab4a46f447f438ceb7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841106"
---
# <a name="mrxlowiosubmitlowio_op_exclusivelock-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\] ルーチン


*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* ルーチンは、ネットワークミニリダイレクターがファイルオブジェクトに対して排他ロックを開くように要求するために[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_EXCLUSIVELOCK](
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* は正常に完了したか、次のいずれかの適切な NTSTATUS 値を\_返します。

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
<td align="left"><p>要求を完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>リモートサーバーから無効な応答を受信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p><em>RxContext</em>で無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>リモートサーバーに再接続して要求を完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンは実装されていません。</p></td>
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

RDBSS は、 *MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* を呼び出します。これに応じて、IRP\_[**MJ\_ロック\_制御**](irp-mj-lock-control.md)要求が発生した場合**に応答します。IrpSp-&gt;フラグ**には、SL\_排他\_ロックビットが設定されています。

*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* を呼び出す前に、RDBSS は、 *RxContext*パラメーターが指す RX\_CONTEXT 構造体の次のメンバーを変更します。

**Lowiocontext. Operation**メンバーは lowio\_OP\_EXCLUSIVELOCK に設定されています。

**Lowiocontext threadid**メンバーは、RDBSS で操作を開始したプロセスのスレッドに設定されます。

QuadPart の値には、 **Lowiocontext** ... byteoffset メンバーは、 **irpsp-&gt;パラメーター**の値に設定されます。

**Lowiocontext. Paramsfor Locks. キー**メンバーは、 **irpsp-&gt;Parameters. lockcontrol. key**の値に設定されます。

**Lowiocontext. Locks. flags**メンバーは、 **irpsp-&gt;フラグ**の値に設定されます。

QuadPart**メンバーには、** irpsp-&gt;パラメーターの値が設定されています. **Lockcontrol. length.** 。

RX\_コンテキスト構造の**Lowiocontext 操作**メンバーは、実行する低 i/o 操作を指定します。 低 i/o ルーチンのいくつかは、ネットワークミニリダイレクターで同じルーチンを指すことができます。これは、この**Lowiocontext 操作**のメンバーが、要求された低 i/o 操作を区別するために使用できるためです。 たとえば、ファイルロックに関連するすべての i/o 呼び出しで、ネットワークミニリダイレクターで同じ低 i/o ルーチンを呼び出すことができ、そのルーチンは**Lowiocontext. operation**メンバーを使用して、要求されたロック操作とロック解除操作を区別できます。

*MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* ルーチンが完了するまでに時間がかかる場合は、ネットワーク通信を開始する前に、ネットワークミニリダイレクタードライバーが FCB 構造体を解放する必要があります。 FCB 構造体は、 [**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)を呼び出すことによって解放できます。 *MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]* ルーチンが処理されている間、RX\_コンテキストの**lowiocontext**スレッドメンバーは、プロセスのスレッドを示すことが保証されます。RDBSS で操作を開始しました。

RX\_コンテキストの**Lowiocontext threadid**メンバーを使用すると、別のスレッドに代わって FCB 構造体を解放できます。 非同期ルーチンが完了すると、初期スレッドから取得された FCB 構造体が解放されます。

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
<td align="left">Mrx .h (Mrx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]** ](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_\_\_ディレクトリの変更を通知\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_読み取り\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_ロック解除\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_ロック解除\_複数\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]** ](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






