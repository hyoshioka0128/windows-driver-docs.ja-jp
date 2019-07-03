---
title: バグ チェック 0xBFF BC_BTHMINI_VERIFIER_FAULT
description: BC_BTHMINI_VERIFIER_FAULT のバグ チェックでは、0x00000BFF の値を持ちます。 これは、Bluetooth ミニポート拡張可能なドライバーの検証ツールが違反をキャッチすることを示します。
ms.assetid: 4BB54209-89EA-455D-B850-CC2A96A43C87
keywords:
- バグ チェック 0xBFF BC_BTHMINI_VERIFIER_FAULT
- BC_BTHMINI_VERIFIER_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BC_BTHMINI_VERIFIER_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c41bc7ecb9b1f81bbcaf3486d40e3a3804907727
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518973"
---
# <a name="bug-check-0xbff-bcbthminiverifierfault"></a>バグ チェック 0xBFF:BC\_BTHMINI\_VERIFIER\_エラー


ビジネス継続性\_BTHMINI\_VERIFIER\_フォールトのバグ チェックが 0x00000BFF の値を持ちます。 これは、Bluetooth ミニポート拡張可能なドライバーの検証ツールが違反をキャッチすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="bcbthminiverifierfault-parameters"></a>BC\_BTHMINI\_VERIFIER\_フォールト パラメーター


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
<td align="left">1</td>
<td align="left"><p>Bluetooth の検証エラーのサブタイプ。</p>
<div class="code">
<code>0x1 : An attempt was made to return a packet with type that mis-matched its original request.
                  2 - Returned packet type
                  3 - Expected packet type
                  4 - Reserved
            0x2 : An attempt was made to return an unexpected status code and caused the packet to be discarded.
                  2 - Unexpected return status
                  3 - Reserved
                  4 - Reserved
            0x3 : Incorrect output buffer size was returned to indicate number of bytes written by the lower transport driver.
                  2 - Unexpected buffer size
                  3 - Expected buffer size
                  4 - Reserved</code>
</div></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
</tbody>
</table>



<a name="resolution"></a>解決方法
----------

パラメーター 1 では、種類の違反について説明します。 不適切な動作のドライバーを特定の呼び出し履歴を確認します。








