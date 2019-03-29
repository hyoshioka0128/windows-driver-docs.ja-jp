---
title: バグ チェック 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
description: DMA_COMMON_BUFFER_VECTOR_ERROR のバグ チェックでは、0x000001DC の値を持ちます。 これは、そのドライバーが DMA のベクトル化一般的なバッファーの Api を誤って使用を示します。
keywords:
- バグ チェック 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
- DMA_COMMON_BUFFER_VECTOR_ERROR
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- DMA_COMMON_BUFFER_VECTOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 297342cf42182e2f006a1b3d2a51c62368c9409d
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743606"
---
# <a name="bug-check-0x1dc-dmacommonbuffervectorerror"></a>バグ チェック 0x1DC の。DMA\_共通\_バッファー\_ベクター\_エラー

DMA\_共通\_バッファー\_ベクター\_エラーのバグ チェックが 0x000001DC の値を持ちます。 これは、ドライバーが DMA のベクトル化一般的なバッファーの Api を誤って使用することを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

## <a name="dmacommonbuffervectorerror-parameters"></a>DMA\_共通\_バッファー\_ベクター\_エラー パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| エラーの種類を示します。 次の値を参照してください。|
|2| 次の値を参照してください。 |
|3| 次の値を参照してください。 |
|4| 次の値を参照してください。 |

**エラーの種類**

```
0x01 : Wrong IRQL
    2 - Current IRQL.

x02 : Vector not empty.
    2 - Index of remaining buffer.
    3 - Virtual Address of remaining buffer.
    4 - Logical address of remaining buffer.

0x03 : Index out of bounds.
    2 - Number of available entries.
    3 - Index requested.

0x04 : Index freed.
    2 - Index requested.

0x05 : Common buffer leaked.
```

## <a name="cause"></a>原因
-----

ドライバーは DMA のベクトル化一般的なバッファーの Api を誤って使用します。

## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

