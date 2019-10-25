---
title: MRxLowIOSubmit \ LOWIO\_OP\_読み取り \ ルーチン
description: MRxLowIOSubmit \ LOWIO\_OP\_READ \ ルーチンは、ネットワークミニリダイレクターに読み取り要求を発行するために、RDBSS によって呼び出されます。
ms.assetid: 26a173d8-e3ab-4c63-8390-133afd35b51a
keywords:
- MRxLowIOSubmit LOWIO_OP_READ ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_READ
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1749ba0d0b811df68876538a3a885688b3832b6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841103"
---
# <a name="mrxlowiosubmitlowio_op_read-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_読み取り\] ルーチン


*MRxLowIOSubmit\[LOWIO\_OP\_read\]* ルーチンは、ネットワークミニリダイレクターに対する読み取り要求を発行するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_READ];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_READ](
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

*MRxLowIOSubmit\[LOWIO\_OP\_読み取り\]* は正常終了時に成功したか、または次のいずれかのような適切な NTSTATUS 値を\_返します。

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
<td align="left"><p>FCB 構造体が取得されましたが、関連付けられている SRV_OPEN 構造体が閉じられています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>要求を完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>無効なデバイス要求が指定されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p><em>RxContext</em>で無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンは実装されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>指定された要求は、ネットワークミニリダイレクターでサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS は、 [**IRP\_MJ\_読み取り**](irp-mj-read.md)要求の受信に応答して、 *MRxLowIOSubmit\[lowio\_OP\_read\]* を呼び出します。

*MRxLowIOSubmit\[LOWIO\_OP\_READ\]* を呼び出す前に、 *RxContext*パラメーターによって示されている RX\_CONTEXT 構造体内の次のメンバーが RDBSS によって変更されます。

**Lowiocontext 操作**のメンバーが LOWIO\_OP\_READ に設定されています。

**Lowiocontext threadid**メンバーは、RDBSS で操作を開始したプロセスのスレッドに設定されます。

**Lowiocontext. ReadWrite. キー**メンバーは、 **irpsp-&gt;パラメーター**の値に設定されます。

READWRITEFLAG**のパラメーター**には LOWIO\_\_PAGING\_io ビットが設定されています。この場合、 **Irp-&gt;フラグ**には、IRP\_ページング\_i/o ビットが設定されています。

IoReadAccess のパラメーターに**は、ユーザー**バッファーのロックが設定されています。

**ByteCount**メンバーは、irpsp-&gt;のパラメーターの値に設定されています。読み取りの長さ。

通常、読み取り要求はかなりの時間がかかるため、非同期操作としてネットワークミニリダイレクターによって実装されます。 通常、この操作は、リモートサーバーへのネットワーク要求の送信で構成されます。 サーバーで読み取り要求が完了すると、応答が取得されます。 これは、ネットワークミニリダイレクターがキャンセル処理をローカルで行うためにコンテキストを登録する必要がある操作の例です。

*MRxLowIOSubmit\[LOWIO\_OP\_READ\]* ルーチンが処理されている間、RX\_コンテキストの**lowiocontext**スレッドメンバーは、を開始したプロセスのスレッドを示すことが保証されます。RDBSS での操作です。 **Lowiocontext threadid**メンバーを使用すると、別のスレッドに代わって FCB 構造体を解放できます。 非同期ルーチンが完了すると、初期スレッドから取得された FCB 構造体が解放されます。 FCB 構造体は、 [**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)を呼び出すことによって解放できます。

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


[**MRxLowIOSubmit\[LOWIO\_OP\_EXCLUSIVELOCK\]** ](mrxlowiosubmit-lowio-op-exclusivelock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]** ](mrxlowiosubmit-lowio-op-fsctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](mrxlowiosubmit-lowio-op-ioctl-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_\_\_ディレクトリの変更を通知\]** ](mrxlowiosubmit-lowio-op-notify-change-directory-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_ロック解除\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_ロック解除\_複数\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]** ](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






