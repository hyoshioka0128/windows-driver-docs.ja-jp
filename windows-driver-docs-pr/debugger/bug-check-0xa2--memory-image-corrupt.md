---
title: Bug Check 0xA2 MEMORY_IMAGE_CORRUPT
description: MEMORY_IMAGE_CORRUPT のバグ チェックでは、0x000000A2 の値を持ちます。 このバグ チェックでは、メモリ内で実行可能ファイルのイメージの破損が検出されたことを示します。
ms.assetid: 73990217-4af2-478c-aa5e-39e6bc5811cf
keywords:
- Bug Check 0xA2 MEMORY_IMAGE_CORRUPT
- MEMORY_IMAGE_CORRUPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MEMORY_IMAGE_CORRUPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f79e50d514e808aa00df9abb2f169ab339c88b15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361672"
---
# <a name="bug-check-0xa2-memoryimagecorrupt"></a>バグ チェック 0xA2:メモリ\_イメージ\_が壊れています


メモリ\_イメージ\_破損バグ チェックが 0x000000A2 の値を持ちます。 このバグ チェックでは、メモリ内で実行可能ファイルのイメージの破損が検出されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="memoryimagecorrupt-parameters"></a>メモリ\_イメージ\_破損しているパラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p><strong>パラメーター 3 が 0 の場合。</strong>失敗したテーブル ページ内のページ番号</p>
<p><strong>パラメーター 3 が 0 以外の場合。</strong>インデックスの実行、障害が発生したページとページ番号</p></td>
<td align="left"><p>0、またはインデックスを実行と一致しませんでした。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>テーブルのページのチェック エラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>範囲の開始の物理的なページ番号</p></td>
<td align="left"><p>ページ単位で、範囲の長さ</p></td>
<td align="left"><p>この実行を含むテーブル ページのページ数</p></td>
<td align="left"><p>表示されているメモリの範囲のチェックサムが正しくありません。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

メモリの範囲に巡回冗長検査 (CRC) チェックに失敗しました。

システム スリープ解除操作でメモリの障害に対する保護をさまざまな領域のメモリをチェックする可能性があります。

 

 




