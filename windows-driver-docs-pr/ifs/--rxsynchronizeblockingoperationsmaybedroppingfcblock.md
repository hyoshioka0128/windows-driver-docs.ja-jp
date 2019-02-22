---
title: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 関数'
description: '\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock では、同じ作業キューにブロッキング I/O 要求を同期します。'
ms.assetid: 350294ca-9790-4996-bcb5-1423db762c6e
keywords:
- インストール可能なファイル システム ドライバーの __RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 関数
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
ms.openlocfilehash: 991df402d7c32af7a2715ec98306653f72b9370b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548587"
---
# <a name="rxsynchronizeblockingoperationsmaybedroppingfcblock-function"></a>\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock 関数


**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**同じ作業キューにブロッキング I/O 要求を同期します。

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

*RxContext* \[入力、出力\]  
RX へのポインター\_同期されている操作のコンテキスト。

*BlockingIoQ* \[入力、出力\]  
リストへのポインター\_キューのエントリ。

*DropFcbLock* \[in\]  
FCB のリソースを解放するかどうかを示すブール値。 このパラメーターが場合**TRUE**、FCB リソースが解放されます。

<a name="return-value"></a>戻り値
------------

**\_\_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**ステータスを返します\_成功、または、次のいずれかなどの適切な NTSTATUS 値に成功しました。

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
<td align="left"><p>I/O 要求と関連付けられている RX_CONTEXT が取り消されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_PENDING</strong></td>
<td align="left"><p><em>RxContext</em> 、非同期操作が、 <em>RxContext</em>がキューに追加されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**ルーチンは、同じ作業キューにブロッキング I/O 要求を同期します。 RDBSS 使用 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**内部的に同期するパイプ操作の名前します。 作業キューが、ファイル オブジェクトに関連付けられている拡張子 (FOBX) によって参照されるキュー、 **pFcb** 、RX のメンバー\_によって示される CONTEXT 構造*RxContext*します。

ネットワークのミニ リダイレクターを使用して、可能性があります **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**ネットワーク ミニリダイレクターによって保持されている別のキューに対する操作を同期します。

場合*RxContext* 、非同期操作のマークが付いて **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**は追加、 *RxContext*キューと状態の戻り値に\_保留します。 場合*RxContext* 、同期処理のマークが付いて **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**ブロックと*RxContext*への呼び出しが行われたときに再開[ **RxResumeBlockedOperations\_順次**](https://msdn.microsoft.com/library/windows/hardware/ff554701)します。

ブロッキング I/O 要求が取り消された場合 **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**ステータスを返します\_キャンセル、エラーを示します。

**SyncEvent** 、RX のメンバー\_によって示される CONTEXT 構造*RxContext*呼び出す前に再設定する必要があります **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**します。 FCB のリソースを呼び出す前にロックする必要があります **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock**場合、 *DropFcbLock* にパラメーターが設定されている**TRUE**します。

呼び出し元の Windows XP と Windows 2000 で次の 2 つのマクロが定義されている **\_ \_RxSynchronizeBlockingOperationsMaybeDroppingFcbLock** :

**RxSynchronizeBlockingOperations** -を呼び出し、 *DropFcbLock*パラメーターに設定**FALSE**します。

**RxSynchronizeBlockingOperationsAndDropFcbLock** -を呼び出し、 *DropFcbLock*パラメーターに設定**TRUE**します。

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
<td align="left"><p>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock ルーチンは、Windows XP および Windows 2000 にできるだけです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Rxcontx.h (Rxcontx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**RxCompleteRequest\_Real**](https://msdn.microsoft.com/library/windows/hardware/ff554348)

[**RxCreateRxContext**](https://msdn.microsoft.com/library/windows/hardware/ff554367)

[**RxDereference**](https://msdn.microsoft.com/library/windows/hardware/ff554388)

[**RxDereferenceAndDeleteRxContext\_Real**](https://msdn.microsoft.com/library/windows/hardware/ff554393)

[**RxInitializeContext**](https://msdn.microsoft.com/library/windows/hardware/ff554502)

[**RxPrepareContextForReuse**](https://msdn.microsoft.com/library/windows/hardware/ff554643)

[**RxResumeBlockedOperations\_順次**](https://msdn.microsoft.com/library/windows/hardware/ff554701)

[**\_\_RxSynchronizeBlockingOperations**](https://msdn.microsoft.com/library/windows/hardware/ff557377)

 

 






