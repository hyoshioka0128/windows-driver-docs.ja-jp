---
title: MRxLowIOSubmit \ LOWIO\_OP\_\_ディレクトリ \ ルーチンへの通知\_変更
description: MRxLowIOSubmit \ LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY \ ルーチンは、ディレクトリ変更通知操作のためにネットワークミニリダイレクターに要求を発行するために、RDBSS によって呼び出されます。
ms.assetid: a3ac7936-7c46-4e46-929a-dc495187a01b
keywords:
- MRxLowIOSubmit LOWIO_OP_NOTIFY_CHANGE_DIRECTORY ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxLowIOSubmit LOWIO_OP_NOTIFY_CHANGE_DIRECTORY
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f7d2e7aff720b3837cdad446ab48f43bcb9b398
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841104"
---
# <a name="mrxlowiosubmitlowio_op_notify_change_directory-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_\_ディレクトリ\] ルーチンに変更を通知\_


*MRxLowIOSubmit\[LOWIO\_OP\_通知\_change\_directory\]* ルーチンは、ディレクトリ変更通知操作のためにネットワークミニリダイレクターに要求を発行するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY];

NTSTATUS MRxLowIOSubmit[LOWIO_OP_NOTIFY_CHANGE_DIRECTORY](
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

*MRxLowIOSubmit\[LOWIO\_OP\_\_変更の通知\_ディレクトリ\]* は成功時に成功したか、適切な NTSTATUS 値 (次のいずれか) を返します。

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

RDBSS は、 [**IRP\_MJ\]directory\_CONTROL**](irp-mj-directory-control.md)要求の受信に応答して、 *MRxLowIOSubmit\[lowio\_OP\_\_DIRECTORY\_の変更を\_に通知*します。

*MRxLowIOSubmit\[LOWIO\_OP\_\_DIRECTORY\]の変更を\_通知*する前に、 *RxContext*パラメーターによって示される RX\_CONTEXT 構造体の次のメンバーが変更されます。

**Lowiocontext 操作**のメンバーは lowio\_OP\_通知\_\_ディレクトリの変更を通知するように設定されています。

**Lowiocontext threadid**メンバーは、RDBSS で操作を開始したプロセスのスレッドに設定されます。

**Irpsp-&gt;フラグ**に SL\_WATCH\_ツリービットが設定されている場合は、 **WatchTree**メンバーが**TRUE**に設定されます。

**Lowiocontext. Paramchangedirectory**のメンバーは、 **irpsp-&gt;Parameters. notifydirectory.** の値に設定されています。

**Lowiocontext. NotifyChangeDirectory. NotificationBufferLength**メンバーは、 **irpsp-&gt;Parameters. Notifydirectory. Length**の値に設定されます。

MmGetSystemAddressForMdlSafe **MdlAddress**および NormalPagePriority で&gt;、を呼び出すことによって返される値に設定されている値に、 **lowiocontext。** ユーザーバッファーもプローブされ、書き込みアクセス用にロックされます。

ディレクトリ変更通知操作は、通常、非同期操作としてネットワークミニリダイレクターによって実装されます。これは、かなりの時間がかかる可能性があるためです。 通常、この操作は、変更通知を要求しているリモートサーバーへのネットワーク要求の送信で構成されます。 この応答は、必要な変更がサーバー上で影響を受ける場合に取得されます。 これは、ネットワークミニリダイレクターがローカルで開始された取り消し処理のために一意のコンテキスト値を登録する必要がある操作の例です。

*MRxLowIOSubmit\[LOWIO\_OP\_\_ディレクトリ\]* ルーチンが処理されていることを通知\_変更しますが、RX\_コンテキストの**Lowiocontext スレッド**メンバーは、RDBSS で操作を開始したプロセスのスレッド。 **Lowiocontext threadid**メンバーを使用すると、別のスレッドに代わって FCB 構造体を解放できます。 非同期ルーチンが完了すると、初期スレッドから取得された FCB 構造体が解放されます。 FCB 構造体は、 [**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)を呼び出すことによって解放できます。

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

[**MRxLowIOSubmit\[LOWIO\_OP\_読み取り\]** ](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]** ](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_ロック解除\]** ](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_ロック解除\_複数\]** ](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_書き込み\]** ](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)

 

 






