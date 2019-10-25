---
title: MRxStop ルーチン
description: TheMRxStop ルーチンは、ネットワークミニリダイレクターを停止するために RDBSS によって呼び出されます。
ms.assetid: 7600335e-ab7c-4993-9e27-18e530496b1c
keywords:
- MRxStop ルーチンのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: b8b4d2b12d52c667eb3caf818ec4dbe0dbd6176e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841066"
---
# <a name="mrxstop-routine"></a>MRxStop ルーチン


*MRxStop*ルーチンは、ネットワークミニリダイレクターを停止するために[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

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

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、ネットワークミニリダイレクターの停止を要求した IRP が含まれます。

*RxDeviceObject* \[in、out\]  
このネットワークミニリダイレクターの RDBSS\_デバイス\_オブジェクト構造へのポインター。

<a name="return-value"></a>戻り値
------------

*MRxStop*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

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
<td align="left"><p>ネットワークミニリダイレクターに開いているハンドルがあるため、この時点では停止できません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>ネットワークミニリダイレクターが開始されませんでした。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*MRxStop*は、RDBSS の観点からネットワークミニリダイレクターを停止して初期化前します。 ネットワークミニリダイレクターを停止すると、メモリ割り当てやその他のシステムリソースが解放される可能性があります。

*MRxStop*を呼び出す前に、RDBSS によって次の値が変更されます。

*RxContext*によってポイントされる RX\_コンテキスト構造の**MajorFunction**メンバーは、IRP のメジャー関数に設定されます。

*RxContext*によってポイントされている RX\_コンテキスト構造の**Lowiocontext のコード**メンバーは、ネットワークミニリダイレクターを停止するために使用された FSTCL 要求の場合、IRP の FsCtl コードに設定されます。

*RxDeviceObject*によってポイントされている RDBSS\_デバイス\_オブジェクト構造の**startstopcontext. State**メンバーは、\_の進行状況で RDBSS\_STOP\_に設定されます。

*RxDeviceObject*によってポイントされるオブジェクト構造の RDBSS\_\_デバイスの**Startstopcontext の pstopcontext**メンバーは、 *RxContext*パラメーターに設定されます。

*MRxStop*は、 [**RXSTOPMINIRDR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)ルーチンから RDBSS によって呼び出されます。

*MRxStop*が STATUS\_SUCCESS を返した場合、ルーチンは成功しました。 その他の戻り値は、ネットワークミニリダイレクターの停止中にエラーが発生したことを示します。

*MRxStop*によって STATUS\_SUCCESS が返された場合、RDBSS は RDBSS の状態を\_RDBSS に設定します。 この状態は、 *RxDeviceObject*によってポイントされるオブジェクト構造\_RDBSS\_デバイスの**startstopcontext. state**メンバーに格納されます。

ネットワークミニリダイレクターは、通常、ネットワークミニリダイレクターが開始されているかどうかを示す内部変数を保持します。 たとえば、ネットワークミニリダイレクターは、停止、開始、および開始操作または停止操作が進行中であることを追跡できます。

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


[**MRxDevFcbXXXControlFile**](mrxdevfcbxxxcontrolfile.md)

[**MrxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)

[**RxStopMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)

 

 






