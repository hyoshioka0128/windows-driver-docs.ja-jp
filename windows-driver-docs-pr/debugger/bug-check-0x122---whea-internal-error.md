---
title: Bug Check 0x122 WHEA_INTERNAL_ERROR
description: WHEA_INTERNAL_ERROR のバグ チェックでは、0x00000122 の値を持ちます。
ms.assetid: b0bf1f27-bfdd-4d5d-aeac-f74f45c6174f
keywords:
- Bug Check 0x122 WHEA_INTERNAL_ERROR
- WHEA_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WHEA_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8df990b5334833c4911dcc8c3a459ff565d4a892
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238881"
---
# <a name="bug-check-0x122-wheainternalerror"></a>バグ チェック 0x122:WHEA\_内部\_エラー


WHEA\_内部\_エラーのバグ チェックが 0x00000122 の値を持ちます。 このバグ チェックでは、Windows ハードウェア エラー アーキテクチャ (WHEA) で内部エラーが発生したことを示します。 エラーには、プラグイン プラットフォーム固有のハードウェア エラー ドライバー (PSHED) の実装でバグを仕入先、ファームウェアの実装のエラー レコード、またはエラー挿入のファームウェアの実装によって提供されることがあります。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="wheainternalerror-parameters"></a>WHEA\_内部\_エラー パラメーター


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
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>メモリのサイズ</p></td>
<td align="left"><p>エラー ソースの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ハードウェア エラーのソース テーブル内のすべてのエラー ソースのための十分なメモリを割り当てられませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>プロセッサの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>プロセッサごとの WHEA 情報ブロックのための十分なメモリを割り当てられませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>状況</p></td>
<td align="left"><p>フェーズ (バグ チェックの初期化フェーズ)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>WHEA では、エラーのソースまたはエラーのソース列挙できませんでした。 十分なメモリを割り当てられませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>状況</p></td>
<td align="left"><p>フェーズ</p></td>
<td align="left"><p>エラー ソースの種類</p></td>
<td align="left"><p>パラメーター 3 で指定されたフェーズ中にエラーの発生元 (パラメーター 4) を初期化できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>状況</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>十分なメモリを割り当てられませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>エラー ソースの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ソース記述子内のすべてのエラーのための十分なメモリを割り当てられませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>エラー ソースの種類</p></td>
<td align="left"><p>ソース ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>WHEA では、無効なエラー ソースから、未修正のエラーのソースを受信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>エラー ソースの種類</p></td>
<td align="left"><p>ソース ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>未修正のエラーのエラー レコードを割り当てられませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>エラー ソースの種類</p></td>
<td align="left"><p>ソース ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>未修正のエラーのエラー レコードの作成に失敗しました。</p></td>
</tr>
</tbody>
</table>

 

パラメーター 1 が 0x6、0x9、0 xa、または 0 xb と等しい場合は、その他のパラメーターのいずれかのエラーのソースの種類が含まれます。 次の表は、エラーのソースの種類、使用可能な値を示します。

| 値 | 説明                          |
|-------|--------------------------------------|
| 0x00  | マシン チェック例外              |
| 0x01  | マシン チェックを修正しました              |
| 0x02  | 修正されたプラットフォーム エラー             |
| 0x03  | 非マスク不可能割り込み               |
| 0x04  | PCI express エラー                    |
| 0x05  | 他の種類のエラーのソース/一般 |
| 0x06  | IA64 の初期化エラーの発生元               |
| 0x07  | 起動エラーのソース                    |
| 0x08  | SCI ベースの一般的なエラーのソース       |
| 0x09  | Itanium マシン チェックの中止          |
| 0x0A  | Itanium マシン チェック                |
| 0x0B  | Itanium は、プラットフォーム エラーの修正     |

 

 

 




