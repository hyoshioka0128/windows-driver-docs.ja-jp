---
title: バグチェック 0x1DC DMA_COMMON_BUFFER_VECTOR_ERROR
description: DMA_COMMON_BUFFER_VECTOR_ERROR のバグチェックの値は0x000001DC です。 これは、ドライバーが DMA ベクトル化された共通バッファー Api を誤用していることを示します。
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
ms.openlocfilehash: 16c5a8a24e70756d33305902c10ec54077aabd03
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916228"
---
# <a name="bug-check-0x1dc-dma_common_buffer_vector_error"></a>バグチェック 0x1DC: DMA\_共通\_バッファー\_VECTOR\_エラー

DMA\_共通\_バッファー\_VECTOR\_エラーのバグチェックには、0x000001DC の値が含まれています。 これは、ドライバーが DMA ベクトル化された共通バッファー Api を誤用したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

 

## <a name="dma_common_buffer_vector_error-parameters"></a>DMA\_共通\_バッファー\_VECTOR\_のエラーパラメーター

|パラメーター|説明|
|-------- |---------- |
|1| エラーの種類を示します。 以下の値を参照してください。|
|2| 以下の値を参照してください。 |
|3| 以下の値を参照してください。 |
|ホーム フォルダーが置かれているコンピューターにアクセスできない| 以下の値を参照してください。 |

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

ドライバーが DMA ベクトル化された共通バッファー Api を誤用しています。 ! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

## <a name="see-also"></a>参照
----------

[バグチェックコードリファレンス](bug-check-code-reference2.md)

