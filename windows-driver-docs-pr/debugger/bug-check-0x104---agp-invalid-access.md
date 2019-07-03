---
title: バグ チェック 0x104 AGP_INVALID_ACCESS
description: AGP_INVALID_ACCESS のバグ チェックでは、0x00000104 の値を持ちます。 これは、GPU が既にコミットされていないポート (AGP) メモリについてする範囲の高速化グラフィックスを記述していることを示します。
ms.assetid: c1f5322e-847a-424f-b117-1714b8572a4f
keywords:
- バグ チェック 0x104 AGP_INVALID_ACCESS
- AGP_INVALID_ACCESS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_INVALID_ACCESS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4ef01ed0620ab573cf2d126b5413744e90b194e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521581"
---
# <a name="bug-check-0x104-agpinvalidaccess"></a>バグ チェック 0x104:AGP\_無効な\_アクセス


AGP\_無効な\_アクセスのバグ チェックが 0x00000104 の値を持ちます。 これは、GPU が既にコミットされていないポート (AGP) メモリについてする範囲の高速化グラフィックスを記述していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="agpinvalidaccess-parameters"></a>AGP\_無効な\_アクセス パラメーター


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
<td align="left"><p>(ULONG) で、AGP 検証ツールのページが破損している最初の ULONG データ内のオフセットします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常、このバグ チェック符号なしまたは不適切なテスト ビデオ ドライバーが原因です。 古い BIOS によっても発生できます。

<a name="resolution"></a>解決方法
----------

ディスプレイ ドライバーとコンピューターの BIOS 更新プログラムを確認します。

 

 




