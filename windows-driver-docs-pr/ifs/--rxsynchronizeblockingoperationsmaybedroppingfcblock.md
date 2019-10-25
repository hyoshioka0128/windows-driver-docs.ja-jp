---
title: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 関数'
description: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock は、ブロックしている i/o 要求を同じ作業キューに同期します。'
ms.assetid: 350294ca-9790-4996-bcb5-1423db762c6e
keywords:
- __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 関数のインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock
api_location:
- rxcontx.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc10cb53121c8a017fdaaca50f49466abd2dc32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841520"
---
# <a name="__rxsynchronizeblockingoperationsmaybedroppingfcblock-function"></a>\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 関数


**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**は、ブロックしている i/o 要求を同じ作業キューに同期します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock(
  _Inout_ PRX_CONTEXT RxContext,
  _Inout_ PLIST_ENTRY BlockingIoQ,
  _In_    BOOLEAN     DropFcbLock
);
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[in、out\]  
同期されている操作の RX\_コンテキストへのポインター。

*BlockingIoQ* \[in、out\]  
キューのリスト\_エントリへのポインター。

\] の*Dropfcblock* \[  
FCB リソースを解放する必要があるかどうかを示すブール値。 このパラメーターが**TRUE**の場合、FCB リソースが解放されます。

<a name="return-value"></a>戻り値
------------

**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**は成功時に成功したか、次のいずれかのような適切な NTSTATUS 値\_を返します。

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
<td align="left"><strong>STATUS_CANCELLED</strong></td>
<td align="left"><p>I/o 要求と関連付けられた RX_CONTEXT が取り消されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>あります</strong></td>
<td align="left"><p><em>RxContext</em>は非同期操作のためのもので、 <em>RxContext</em>がキューに追加されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**ルーチンは、ブロッキング i/o 要求を同じ作業キューに同期します。 RDBSS は、内部的に\_を使用して名前付きパイプ操作を同期するために、 **\_** を使用します。 作業キューは、 *RxContext*によってポイントされる RX\_コンテキスト構造の**pfcb**メンバーに関連付けられているファイルオブジェクト拡張機能 (fobx) によって参照されるキューです。

ネットワークミニリダイレクターは **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**を使用して、ネットワークミニリダイレクターによって管理されている別のキューで操作を同期できます。

*RxContext*が非同期操作用にマークされている場合は、 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**によって、 *RxContext*がキューに追加され、STATUS\_PENDING が返されます。 *RxContext*が同期操作用にマークされている場合、 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**はブロックされ、RxResumeBlockedOperations への呼び出しが行われると*RxContext*が再開され[ **\_順次**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)。

ブロッキング i/o 要求が取り消された場合、 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**は、エラーを示す状態\_キャンセルを返します。

*RxContext*が指す RX\_コンテキスト構造の**syncevent**メンバーは、 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**を呼び出す前にリセットされている必要があります。 *Dropfcblock*パラメーターが**TRUE**に設定されている場合は、 **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**を呼び出す前に、FCB リソースをロックする必要があります。

次の2つのマクロは、Windows XP と Windows 2000 で **\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**を呼び出すために定義されています。

**RxSynchronizeBlockingOperations** - *dropfcblock*パラメーターを**FALSE**に設定してを呼び出します。

**RxSynchronizeBlockingOperationsAndDropFcbLock** - *dropfcblock*パラメーターを**TRUE**に設定してを呼び出します。

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
<td align="left"><p>バージョン</p></td>
<td align="left"><p>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock ルーチンは、Windows XP および Windows 2000 でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Rxcontx (Rxcontx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**RxCompleteRequest\_Real**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real)

[**RxCreateRxContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext)

[**RxDereference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)

[**RxDereferenceAndDeleteRxContext\_Real**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)

[**RxInitializeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext)

[**RxPrepareContextForReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse)

[**RxResumeBlockedOperations\_順次**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)

[ **\_\_RxSynchronizeBlockingOperations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)

 

 






