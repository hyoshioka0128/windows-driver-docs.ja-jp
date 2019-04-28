---
title: バグ チェック 0x34 CACHE_MANAGER
description: CACHE_MANAGER のバグ チェックでは、0x00000034 の値を持ちます。 これは、ファイル システムのキャッシュ マネージャーで問題が発生したことを示します。
ms.assetid: a943e5ce-0be7-4b30-94e7-3e29ce8aa38c
keywords:
- バグ チェック 0x34 CACHE_MANAGER
- CACHE_MANAGER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CACHE_MANAGER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eea687d208bba24061d44244a7ad2354c40d734c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361642"
---
# <a name="bug-check-0x34-cachemanager"></a>バグ チェック 0x34:キャッシュ\_マネージャー


キャッシュ\_MANAGER バグ チェックが 0x00000034 の値を持ちます。 これは、ファイル システムのキャッシュ マネージャーで問題が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="cachemanager-parameters"></a>キャッシュ\_マネージャーのパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>ソース ファイルと行番号情報を指定します。 上位 16 ビット ("0 x"の後に最初の 4 つの 16 進数字) は、その識別子番号によってソース ファイルを特定します。 下位 16 ビットは、バグ チェックが発生したファイル内のソース行を特定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックの 1 つの考えられる原因は、非ページ プール メモリの不足です。 非ページ プール メモリは完全になくなると、このエラーは、システムを停止できます。 ただし、インデックス作成のプロセス中に使用可能な非ページ プール メモリの量が非常に低い場合別のカーネル モード ドライバーを非ページ プール メモリを必要とすることができますもこのエラーをトリガーします。

<a name="resolution"></a>解決方法
----------

**非ページ プール メモリの枯渇問題を解決するには。** コンピューターに新しい物理メモリを追加します。 これにより、カーネルで使用できる非ページ プール メモリの量が増加します。

 

 




