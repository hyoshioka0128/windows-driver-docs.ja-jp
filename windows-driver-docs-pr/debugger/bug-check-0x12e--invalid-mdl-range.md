---
title: バグ チェック 0x12E INVALID_MDL_RANGE
description: INVALID_MDL_RANGE のバグ チェックでは、0x0000012E の値を持ちます。
ms.assetid: 911192DC-17B8-4D75-A96E-2E310B30348F
keywords:
- バグ チェック 0x12E INVALID_MDL_RANGE
- INVALID_MDL_RANGE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_MDL_RANGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e20697409442c844c388f6865ca304b5a0d0855f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351366"
---
# <a name="bug-check-0x12e-invalidmdlrange"></a>バグ チェック 0x12E:無効な\_MDL\_範囲


無効な\_MDL\_範囲のバグ チェックが 0x0000012E の値を持ちます。 これは、指定された仮想アドレスの範囲はソース MDL の範囲がドライバーが IoBuildPartialMdl() 関数を呼び出すし、MDL MDL、ソースの一部をマップする、渡されたことを示します。 これは、通常、ドライバーのバグです。

マップにアドレス範囲の長さだけでなく、ソースとターゲットの MDLs は IoBuildPartialMdl() 関数に引数つまり;)。

```cpp
IoBuildPartialMdl(
        IN PMDL SourceMdl,
        IN OUT PMDL TargetMdl,
        IN PVOID VirtualAddress,
        IN ULONG Length
```

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="invalidmdlrange-parameters"></a>無効な\_MDL\_範囲パラメーター


| パラメーター | 説明    |
|-----------|----------------|
| 1         | SourceMdl      |
| 2         | TargetMdl      |
| 3         | virtualAddress |
| 4         | 長さ         |

 

 

 




