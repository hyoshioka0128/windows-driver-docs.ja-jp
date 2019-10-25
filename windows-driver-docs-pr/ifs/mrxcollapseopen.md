---
title: MRxCollapseOpen ルーチン
description: MRxCollapseOpen ルーチンは RDBSS によって呼び出され、ネットワークミニリダイレクターが開いているファイルシステム要求を既存の SRV\_オープン構造に折りたたんでいることを要求します。
ms.assetid: 1c06b2f4-b44a-4d8a-9205-987be1e497ad
keywords:
- MRxCollapseOpen ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxCollapseOpen
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e7bf5be964d2d84033390ba4137db9faa13f0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841116"
---
# <a name="mrxcollapseopen-routine"></a>MRxCollapseOpen ルーチン


*MRxCollapseOpen*ルーチンは[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出され、ネットワークミニリダイレクターが開いているファイルシステム要求を既存の SRV\_オープン構造に折りたたんでいることを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCollapseOpen;

NTSTATUS MRxCollapseOpen(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxCollapseOpen*は正常に完了した状態\_成功したか、次のような適切な NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターンコード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>操作を完了するためのリソースが不足しています。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

*MRxCollapseOpen*は、SRV\_開いている構造体をローカルに折りたたむために RDBSS によって呼び出されます。 ネットワークミニリダイレクターは、折りたたみが可能かどうかを判断するために調査されるため、ネットワークミニリダイレクターを2回呼び出す理由はありません。 ネットワークミニリダイレクターが SRV\_開いている構造を折りたたむ場合は、その操作を行い、返却可能の状態を返します。 STATUS\_SUCCESS の戻り値は、終了する戻り値です。 異なる戻り値 (たとえば、STATUS\_MORE\_PROCESSING\_REQUIRED) は、終了しない戻り値と見なされます。

*MRxCollapseOpen*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**pRelevantSrvOpen**は、折りたたまれるように SRV\_オープン構造に設定されています。

**Create. pSrvCall**は、開いている srv\_に関連付けられている SRV\_呼び出し構造に設定されます。

ネットワークミニリダイレクターが SRV\_開いている構造体を折りたたむ場合は、RX\_コンテキスト構造の**Srvopen**メンバーを、折りたたまれた SRV\_open 構造体に設定する必要があります。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲットプラットフォーム</p></td>
<td align="left">デスクトップ</td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Mrx .h (Mrx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






