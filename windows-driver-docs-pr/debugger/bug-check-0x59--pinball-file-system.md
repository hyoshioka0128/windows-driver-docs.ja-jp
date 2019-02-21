---
title: バグ チェック 0x59 PINBALL_FILE_SYSTEM
description: PINBALL_FILE_SYSTEM のバグ チェックでは、0x00000059 の値を持ちます。 これは、ピンボールのファイル システムで問題が発生したことを示します。
ms.assetid: b6b9f2e9-261d-4d4d-b282-41fadd0bf8b3
keywords:
- バグ チェック 0x59 PINBALL_FILE_SYSTEM
- PINBALL_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PINBALL_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b57675de4fd62e266f46652cf5315b188c7958ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557866"
---
# <a name="bug-check-0x59-pinballfilesystem"></a>バグ チェック 0x59 の。ピンボール\_ファイル\_システム


ピンボール\_ファイル\_システムのバグ チェックが 0x00000059 の値を持ちます。 これは、ピンボールのファイル システムで問題が発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="pinballfilesystem-parameters"></a>ピンボール\_ファイル\_システム パラメーター


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
<td align="left"><p>ソース ファイルと行番号情報を指定します。 上位 16 ビット (後の最初の 4 つの 16 進、 &quot;0 x&quot;) 識別子番号でソース ファイルを識別します。 下位 16 ビットは、バグ チェックが発生したファイル内のソース行を特定します。</p></td>
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

 

 




