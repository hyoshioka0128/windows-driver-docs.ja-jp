---
title: MRxCollapseOpen ルーチン
description: MRxCollapseOpen ルーチンは、ネットワークのミニ リダイレクターが既存の SRV に開いているファイル システムの要求を折りたたむことを要求する RDBSS によって呼び出されます。\_オープン構造体。
ms.assetid: 1c06b2f4-b44a-4d8a-9205-987be1e497ad
keywords:
- MRxCollapseOpen ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: b430112cd814ab7801a285a0c2195dd7e9c8bc85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574810"
---
# <a name="mrxcollapseopen-routine"></a>MRxCollapseOpen ルーチン


*MRxCollapseOpen*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターが既存の SRV に開いているファイル システムの要求を折りたたむことを要求する\_オープン構造体。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCollapseOpen;

NTSTATUS MRxCollapseOpen(
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

*MRxCollapseOpen*ステータスを返します\_次のよう、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>操作を完了するリソースの不足が発生しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

*MRxCollapseOpen*折りたたむには、SRV RDBSS によって呼び出される\_構造をローカルで開く。 ネットワークのミニ リダイレクターはネットワーク ミニリダイレクターを 2 回呼び出す必要はありませんので、折りたたみが可能であるか判断に問い合わせます。 ネットワークのミニ リダイレクターを折りたたむには、SRV 決定かどうか\_ようにはして返すことができる状態に戻す構造体を開きます。 状態の戻り値\_成功した場合は、終端の戻り値。 状態など、さまざまな戻り値、\_詳細\_処理\_REQUIRED は、未終了の戻り値と見なされます。

呼び出しの前に*MRxCollapseOpen*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**pRelevantSrvOpen** 、SRV に設定されている\_を折りたたむ構造体を開きます。

**Create.pSrvCall** 、SRV に設定されている\_呼び出しの構造に関連付けられた、SRV\_開きます。

ネットワークのミニ リダイレクターを折りたたむには、SRV 決定かどうか\_構造体の開く、 **SrvOpen** 、RX のメンバー\_CONTEXT 構造は、折りたたまれた SRV に設定する必要があります\_オープン構造体。

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


[**MRxAreFilesAliased**](https://msdn.microsoft.com/library/windows/hardware/ff549838)

[**MRxCleanupFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549841)

[**MRxCloseSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff549845)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://msdn.microsoft.com/library/windows/hardware/ff549871)

[**MRxDeallocateForFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549872)

[**MRxExtendForCache**](https://msdn.microsoft.com/library/windows/hardware/ff549878)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






