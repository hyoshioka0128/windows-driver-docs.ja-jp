---
title: バグチェック 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
description: DMA_COMMON_BUFFER_VECTOR_ERROR バグチェックの値は0x000001DC です。 これは、ドライバーが DMA ベクトル化された共通バッファー Api を誤用していることを示します。
keywords:
- バグチェック 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
- DMA_COMMON_BUFFER_VECTOR_ERROR
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- DMA_COMMON_BUFFER_VECTOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 140a35037a32191fae10658e1ae6d5ba94d5ede1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534829"
---
# <a name="bug-check-0x1dc-dma_common_buffer_vector_error"></a>バグチェック 0x1DC: DMA \_ 共通 \_ バッファー \_ ベクター \_ エラー

DMA \_ 共通 \_ バッファーベクターエラーのバグチェックには、 \_ \_ 0x000001dc の値が指定されています。 これは、ドライバーが DMA ベクトル化された共通バッファー Api を誤用したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

 

## <a name="dma_common_buffer_vector_error-parameters"></a>DMA \_ 共通 \_ バッファー \_ ベクターの \_ エラーパラメーター

|パラメーター|説明|
|-------- |---------- |
|1| エラーの種類を示します。 以下の値を参照してください。|
|2| 以下の値を参照してください。 |
|3| 以下の値を参照してください。 |
|4| 以下の値を参照してください。 |

**エラーの種類**

```text
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

ドライバーが DMA ベクトル化された共通バッファー Api を誤用しています。 ! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

## <a name="see-also"></a>参照
----------

[バグ チェック コード リファレンス](bug-check-code-reference2.md)

