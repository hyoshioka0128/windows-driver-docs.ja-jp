---
title: バグ チェック 0x106 AGP_ILLEGALLY_REPROGRAMMED
description: AGP_ILLEGALLY_REPROGRAMMED のバグ チェックでは、0x00000106 の値を持ちます。 これは、高速化グラフィックス ポート (AGP) ハードウェアが、承認されていないエージェントによって再プログラムされていることを示します。
ms.assetid: 7acccf9b-bc4f-4842-a332-1023ab26f03d
keywords:
- バグ チェック 0x106 AGP_ILLEGALLY_REPROGRAMMED
- AGP_ILLEGALLY_REPROGRAMMED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_ILLEGALLY_REPROGRAMMED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 667336a210af49d5385e5ee8e1af47b32e0135ff
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521584"
---
# <a name="bug-check-0x106-agpillegallyreprogrammed"></a>バグ チェック 0x106:AGP\_不法\_REPROGRAMMED


AGP\_不法\_REPROGRAMMED バグ チェックが 0x00000106 の値を持ちます。 これは、高速化グラフィックス ポート (AGP) ハードウェアが、承認されていないエージェントによって再プログラムされていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="agpillegallyreprogrammed-parameters"></a>AGP\_ILLEGALLY\_REPROGRAMMED Parameters


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
<td align="left"><p>AGP 下手順の最初のコマンドは、値を登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>現在のコマンドのレジスタの値</p></td>
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

通常、このバグ チェックは、符号なし、または不適切なテスト、ビデオが原因ドライバー。

<a name="resolution"></a>解決方法
----------

更新されたディスプレイ ドライバーのビデオの製造元の Web サイトを確認するか、VGA モードを使用します。

 

 




