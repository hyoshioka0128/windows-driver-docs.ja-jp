---
title: MRxShouldTryToCollapseThisOpen ルーチン
description: MRxShouldTryToCollapseThisOpen ルーチンは RDBSS によって呼び出され、ネットワークミニリダイレクターが、開いている要求を既存のファイルシステムオブジェクトに対して試行するかどうかを示すことを要求します。
ms.assetid: a68755c1-73f5-4134-b506-2a0163637a13
keywords:
- MRxShouldTryToCollapseThisOpen ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxShouldTryToCollapseThisOpen
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeed09a83fa2ef39ad224f661c7b7093e492defb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841069"
---
# <a name="mrxshouldtrytocollapsethisopen-routine"></a>MRxShouldTryToCollapseThisOpen ルーチン


*MRxShouldTryToCollapseThisOpen*ルーチンは[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出され、ネットワークミニリダイレクターが、開いている要求を既存のファイルシステムオブジェクトに対して試行するかどうかを示すことを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxShouldTryToCollapseThisOpen;

NTSTATUS MRxShouldTryToCollapseThisOpen(
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

*MRxShouldTryToCollapseThisOpen*は正常に完了した状態\_成功したか、次のような適切な NTSTATUS 値を返します。

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
<td align="left"><strong>STATUS_MORE_PROCESSING_REQUIRED</strong></td>
<td align="left"><p>ネットワークミニリダイレクターはこの値を返して、開いている要求の折りたたみを無効にします。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*MRxShouldTryToCollapseThisOpen*は、開いている要求を折りたたむ必要があるかどうかを判断するために呼び出されます。

*MRxShouldTryToCollapseThisOpen*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**PRelevantSrvOpen**メンバーは、開いている SRV\_に設定されます。

*MRxShouldTryToCollapseThisOpen*の呼び出しは、ディレクトリの変更通知要求である可能性があります。 そのため、ネットワークミニリダイレクターは、変更通知が正しく機能するように、開いている要求を折りたたむことができない可能性があります。

RX\_コンテキスト構造の RDBSS メンバーに、\_BACKUP\_インテントオプションまたはファイル\_削除用の\_を開く\_が含まれている場合は、[折りたたみ**を**許可しない] が開き\_\_閉じるオプションセットです。

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


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






