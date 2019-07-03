---
title: バグ チェック 0xBFE BC_BLUETOOTH_VERIFIER_FAULT
description: BC_BLUETOOTH_VERIFIER_FAULT のバグ チェックでは、0x00000BFE の値を持ちます。 これは、ドライバーの違反が原因となったことを示します。
ms.assetid: EC1368CE-46A2-4B69-8405-3118503D35C2
keywords:
- バグ チェック 0xBFE BC_BLUETOOTH_VERIFIER_FAULT
- BC_BLUETOOTH_VERIFIER_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BC_BLUETOOTH_VERIFIER_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a668e29912a169b23f1a44350581d51af321332
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518977"
---
# <a name="bug-check-0xbfe-bcbluetoothverifierfault"></a>バグ チェック 0xBFE:BC\_BLUETOOTH\_VERIFIER\_エラー


ビジネス継続性\_BLUETOOTH\_VERIFIER\_フォールトのバグ チェックが 0x00000BFE の値を持ちます。 これは、ドライバーの違反が原因となったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="bcbluetoothverifierfault-parameters"></a>BC\_BLUETOOTH\_VERIFIER\_フォールト パラメーター


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
<code>0x1 : An attempt was made to submit a Bluetooth Request Block that is already in use
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x2 : An attempt was made to free a Bluetooth Request Block that is in use
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x3 : An attempt was made to allocate or initialize an invalid BRB type
                  2 - Brb pointer
                  3 - pdo extension (if available)
                  4 - Reserved
            0x4 : Invalid Bluetooth Request Block pointer was submitted
                  2 - Brb pointer
                  3 - Reserved
                  4 - Reserved
            0x5 : A Bluetooth Request Block with an invalid size was submitted
                  2 - Brb pointer
                  3 - Actual Size
                  4 - Expected Size
            0x6 : The IOCTL_BTH_GET_DEVICE_INFO was called with invalid parameters
                  2 - Reserved
                  3 - Reserved
                  4 - Reserved
            0x7 : BRB_L2CA_UNREGISTER_SERVER was submitted with an invalid server handle
                  2 - Server handle
                  3 - Reserved
                  4 - Reserved
            0x8 : BRB_L2CA_CLOSE_CHANNEL was submitted with an invalid channel handle
                  2 - Brb pointer
                  3 - Channel handle
                  4 - Reserved
            0x9 : BRB_SCO_UNREGISTER_SERVER was submitted with an invalid server handle
                  2 - Server handle
                  3 - Reserved
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








