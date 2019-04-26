---
title: バグ チェック 0xA4 CNSS_FILE_SYSTEM_FILTER
description: CNSS_FILE_SYSTEM_FILTER のバグ チェックでは、0x000000A4 の値を持ちます。 このバグ チェックでは、CNSS ファイル システム フィルターで問題が発生したことを示します。
ms.assetid: fbf04b17-424c-4b9b-beae-5327d20bf0b9
keywords:
- バグ チェック 0xA4 CNSS_FILE_SYSTEM_FILTER
- CNSS_FILE_SYSTEM_FILTER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CNSS_FILE_SYSTEM_FILTER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 576648c2109492a229570a127fbe8cf4e190423e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347212"
---
# <a name="bug-check-0xa4-cnssfilesystemfilter"></a>バグ チェック 0xA4:CNSS\_ファイル\_システム\_フィルター


CNSS\_ファイル\_システム\_フィルターのバグ チェックが 0x000000A4 の値を持ちます。 このバグ チェックでは、CNSS ファイル システム フィルターで問題が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="cnssfilesystemfilter-parameters"></a>CNSS\_ファイル\_システム\_フィルター パラメーター


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

CNSS\_ファイル\_システム\_フィルターのバグ チェックは、非ページ プール メモリがいっぱいのために発生する可能性があります。 非ページ プール メモリが完全にいっぱいの場合は、このエラーは、システムを停止できます。 ただし、インデックス作成のプロセス中に使用可能な非ページ プール メモリの量が非常に低い場合は別のカーネル モード ドライバーを非ページ プール メモリを必要とすることができますもこのエラーをトリガーします。

<a name="resolution"></a>解決方法
----------

**非ページ プール メモリの枯渇問題を解決するには。** コンピューターに新しい物理メモリを追加します。 このメモリ sincrease カーネルで使用できる非ページ プール メモリの量。

 

 




