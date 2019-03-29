---
title: MRxLowIOSubmit\ LOWIO\_OP\_NOTIFY\_CHANGE\_DIRECTORY\ routine
description: MRxLowIOSubmit\ LOWIO\_OP\_通知\_変更\_DIRECTORY\ ルーチンは、ディレクトリ変更通知操作のネットワークのミニ リダイレクターに要求を発行する RDBSS によって呼び出されます。
ms.assetid: a3ac7936-7c46-4e46-929a-dc495187a01b
keywords:
- MRxLowIOSubmit LOWIO_OP_NOTIFY_CHANGE_DIRECTORY ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: b70fbc346cf6039e070973e4c4c82c3c3e9e5338
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582705"
---
# <a name="mrxlowiosubmitlowioopnotifychangedirectory-routine"></a>MRxLowIOSubmit\[LOWIO\_OP\_通知\_変更\_ディレクトリ\]ルーチン


*MRxLowIOSubmit\[LOWIO\_OP\_通知\_変更\_ディレクトリ\]* ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)にディレクトリ変更通知の操作のネットワークのミニ リダイレクターに要求を発行します。

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

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxLowIOSubmit\[LOWIO\_OP\_通知\_変更\_ディレクトリ\]* ステータスを返します\_成功成功時または NTSTATUS の適切な値にこのような次のいずれかとして。

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

 

<a name="remarks"></a>コメント
-------

RDBSS 呼び出し*MRxLowIOSubmit\[LOWIO\_OP\_通知\_変更\_ディレクトリ\]* 受信に応答する[ **IRP\_MJ\_ディレクトリ\_コントロール**](irp-mj-directory-control.md)要求。

呼び出しの前に*MRxLowIOSubmit\[LOWIO\_OP\_通知\_変更\_ディレクトリ\]*、RDBSSRXでは、次のメンバーを変更します。\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**LowIoContext.Operation** LOWIO にメンバーが設定されている\_OP\_通知\_変更\_ディレクトリ。

**LowIoContext.ResourceThreadId**メンバー RDBSS で操作を開始したプロセスのスレッドに設定されます。

**LowIoContext.ParamsFor.NotifyChangeDirectory.WatchTree**に設定されているメンバー **TRUE**場合、 **IrpSp -&gt;フラグ**が、SL\_ウォッチ\_ツリー ビットが設定されます。

**LowIoContext.ParamsFor.NotifyChangeDirectory.CompletionFilter**メンバーの値に設定されます**IrpSp -&gt;Parameters.NotifyDirectory.CompletionFilter**します。

**LowIoContext.ParamsFor.NotifyChangeDirectory.NotificationBufferLength**メンバーの値に設定されます**IrpSp -&gt;Parameters.NotifyDirectory.Length**します。

**LowIoContext.ParamsFor.NotifyChangeDirectory.pNotificationBuffer**メンバーの呼び出しによって返される値に設定されます**MmGetSystemAddressForMdlSafe**を渡して、 **Irp&gt;MdlAddress** NormalPagePriority とします。 ユーザー バッファーもプローブは、書き込みアクセス用にロックします。

ディレクトリ変更通知の操作を通常によって実装されますミニリダイレクター ネットワークは、非同期操作としてかなりの時間がかかるため。 操作は、通常、変更通知を要求しているリモート サーバーにネットワーク要求を送信するので構成されます。 サーバーで、必要な変更の影響を受ける場合は、応答が取得されます。 これは、ローカルで開始されたキャンセルを処理するための一意のコンテキスト値を登録する必要がありますネットワーク ミニリダイレクター操作の例です。

中に、 *MRxLowIOSubmit\[LOWIO\_OP\_通知\_変更\_ディレクトリ\]* ルーチンは、処理中、 **LowIoContext.ResourceThreadId** RX のメンバー\_コンテキスト RDBSS で操作を開始したプロセスのスレッドを示すことが保証されます。 **LowIoContext.ResourceThreadId**別のスレッドの代わり FCB 構造体を解放するメンバーを使用することができます。 非同期のルーチンが完了したら、最初のスレッドから取得された FCB 構造体を解放できます。 FCB 構造体を呼び出すことによって解放できます[ **RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)します。

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

[**MRxLowIOSubmit\[LOWIO\_OP\_READ\]**](mrxlowiosubmit-lowio-op-read-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_SHAREDLOCK\]**](mrxlowiosubmit-lowio-op-sharedlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\]**](mrxlowiosubmit-lowio-op-unlock-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_UNLOCK\_MULTIPLE\]**](mrxlowiosubmit-lowio-op-unlock-multiple-.md)

[**MRxLowIOSubmit\[LOWIO\_OP\_WRITE\]**](mrxlowiosubmit-lowio-op-write-.md)

[**RxReleaseFcbResourceForThreadInMRx**](https://msdn.microsoft.com/library/windows/hardware/ff554694)

 

 






