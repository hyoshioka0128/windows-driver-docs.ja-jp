---
title: C28750
description: Lstrlen とそのバリエーションの C28750 禁止の使用状況を警告します。
ms.assetid: 5057FE71-286A-4710-922F-DFC639717C75
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28750
ms.openlocfilehash: a4f429c51ec7978b617049e6cad163037ce65e5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374736"
---
# <a name="c28750"></a>C28750


C28750 を警告します。Lstrlen とそのバリエーションの禁止された使用状況

この警告は、関数が使用されていることを禁止されておりより優れた置換を示します。

Lstrlen 関数との関連するバリエーションは、操作中に発生する例外の送信に失敗します。 後で、可能性のあるを診断するエラー条件を難しく、別のスレッドで発生するエラー条件がある可能性があります。 さらに、同等の代替関数は、コンパイラによって最適化でき、例外ハンドラーのパフォーマンスのオーバーヘッドを回避 ( **\_お試しください**と **\_を除く**ブロック)。

例外の送信に失敗したため、ライブラリ関数とそのバリアントが禁止されています。 適切な軽減策は、別の文字列の長さの関数に変換する (通常は strlen、wcslen、 \_tcslen)。 ただし、ライブラリの変更を確認するときに、文字列バッファーが信頼されているコードから送信されたこと確認してください。 信頼されていないデータを扱う場合 strlen ファミリは、信頼されていないデータ ブロックの境界を越えるしないことを確認する strnlen ファミリ (または StringCchLength ファミリ) 関数の代わりに切り替えてください。

Lstrlen とは異なり none、置換の例外をキャッチします。 さらに、ライブラリで、NULL ポインターであるため、strlen または strnlen lstrlen を置換するときに、明示的な NULL チェックのコードでは、そのポイントが必要な NULL ポインターがで可能な場合。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">API</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="lstrlen"></span><span id="LSTRLEN"></span>lstrlen</p></td>
<td align="left"><p>信頼されたデータ交換用のオプション: _tcslen</p>
<p>データ交換を信頼されていない: _tcsnlen、StringCchLength</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="lstrlenA"></span><span id="lstrlena"></span><span id="LSTRLENA"></span>lstrlenA</p></td>
<td align="left"><p>信頼されたデータ交換用のオプション: strlen</p>
<p>データ交換を信頼されていない: strnlen、StringCchLengthA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="lstrlenW"></span><span id="lstrlenw"></span><span id="LSTRLENW"></span>lstrlenW</p></td>
<td align="left"><p>信頼されたデータ交換用のオプション: wcslen</p>
<p>データ交換を信頼されていない: wcsnlen、StringCchLengthW</p></td>
</tr>
</tbody>
</table>

 

 

 





