---
title: MRxTruncate ルーチン
description: MRxTruncate ルーチンは、ネットワークのミニ リダイレクターがファイル システム オブジェクトの内容を切り捨てることを要求する RDBSS によって呼び出されます。
ms.assetid: d60ec8ef-2ccf-42ad-97d2-1aaf9d60acfb
keywords:
- MRxTruncate ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxTruncate
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eab5c14bdc506122a9c05e0c509d96a812733f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386083"
---
# <a name="mrxtruncate-routine"></a>MRxTruncate ルーチン


*MRxTruncate*ルーチンを呼び出して[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)ネットワーク ミニ リダイレクターがファイル システム オブジェクトの内容を切り捨てることを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxTruncate;

NTSTATUS MRxTruncate(
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

*MRxTruncate*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>このルーチンが実装されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*MRxTruncate*の両方の次の条件に該当する場合に、クリーンアップ操作の一部として呼び出されます。

-   ディスク ファイルまたはディレクトリに対応するファイル オブジェクト

-   これは、クリーンアップの最後の呼び出しと、切り捨てがマークされているファイル オブジェクト。

場合の切り捨て、ファイル オブジェクトがマークされている、 **fcbstate** FCB 構造体のメンバーが、FCB\_状態\_TRUNCATE\_ON\_閉じるビットが設定されます。 RDBSS は後でキャッシュのマップを初期化します。

呼び出し*MRxTruncate*への呼び出しに続いて[ **MRxCleanupFobx** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))クリーンアップ操作の一部として。

戻り値を無視する RDBSS *MRxTruncate*します。

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


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






