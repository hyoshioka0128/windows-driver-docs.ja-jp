---
title: MRxStop ルーチン
description: TheMRxStop ルーチンは、ネットワークのミニ リダイレクターを停止する RDBSS によって呼び出されます。
ms.assetid: 7600335e-ab7c-4993-9e27-18e530496b1c
keywords:
- MRxStop ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN_CTX
topic_type:
- apiref
api_name:
- MRxStop
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6823f929ad1c0951ae30e15fb0087209dbba542a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379471"
---
# <a name="mrxstop-routine"></a>MRxStop ルーチン


*MRxStop*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニリダイレクターを停止します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN_CTX MRxStop;

NTSTATUS MRxStop(
  _Inout_ PRX_CONTEXT          RxContext,
  _Inout_ PRDBSS_DEVICE_OBJECT RxDeviceObject
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、要求を停止するネットワークのミニ リダイレクター IRP が含まれています。

*RxDeviceObject* \[入力、出力\]  
RDBSS へのポインター\_デバイス\_ネットワークをミニ リダイレクターのオブジェクトの構造体。

<a name="return-value"></a>戻り値
------------

*MRxStop*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_REDIRECTOR_HAS_OPEN_HANDLES</strong></td>
<td align="left"><p>ネットワークのミニ リダイレクターが、この時点で停止することを防ぐことが開いているハンドル。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>ネットワークのミニ リダイレクターは開始されませんでした。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*MRxStop*を停止し、ネットワークのミニ リダイレクター RDBSS の観点からの初期化を解除します。 ネットワークのミニ リダイレクターを停止では、メモリの割り当てとその他のシステム リソースを解放する必要があります可能性があります。

呼び出しの前に*MRxStop*RDBSS は、次の値を変更します。

**MajorFunction** 、RX でメンバー\_によって示される CONTEXT 構造*RxContext*は IRP の主要な関数に設定します。

**LowIoContext.ParamsFor.FsCtl.FsControlCode** 、RX でメンバー\_によって示される CONTEXT 構造*RxContext*これは、FSTCL 要求を使用して停止する場合、IRP の FSCTL コードに設定されますネットワーク ミニのリダイレクターです。

**StartStopContext.State** 、RDBSS のメンバー\_デバイス\_によって示されるオブジェクトの構造*RxDeviceObject* RDBSS に設定されている\_停止\_IN\_進行状況

**StartStopContext.pStopContext** 、RDBSS のメンバー\_デバイス\_によって示されるオブジェクトの構造*RxDeviceObject*に設定されている、 *RxContext*パラメーター。

*MRxStop*から RDBSS によって呼び出される、 [ **RxStopMinirdr** ](https://msdn.microsoft.com/library/windows/hardware/ff554743)ルーチン。

場合*MRxStop*ステータスを返します\_成功すると、そのルーチンが成功しました。 その他の戻り値は、ネットワークのミニ リダイレクターを停止でエラーが発生したことを示します。

場合*MRxStop*ステータスを返します\_RDBSS に成功すると、RDBSS の設定の RDBSS 状態\_STARTABLE します。 この状態は、 **StartStopContext.State** 、RDBSS のメンバー\_デバイス\_によって示されるオブジェクトの構造*RxDeviceObject*します。

ネットワークのミニ リダイレクターは、ネットワークのミニ リダイレクターが開始したかどうかを示す内部変数を保持して通常します。 など、開始、停止されるとき、および操作の開始または停止操作が進行中、ネットワークのミニ リダイレクターは追跡可能性があります。

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


[**MRxDevFcbXXXControlFile**](mrxdevfcbxxxcontrolfile.md)

[**MrxStart**](https://msdn.microsoft.com/library/windows/hardware/ff550829)

[**RxStopMinirdr**](https://msdn.microsoft.com/library/windows/hardware/ff554743)

 

 






