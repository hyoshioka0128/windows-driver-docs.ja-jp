---
title: XR_BIAS カラー チャネルの変換規則
description: XR_BIAS カラー チャネルの変換規則
ms.assetid: B3014241-A86A-4B6E-BC9D-50057B924D98
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49f073b4c9a5dc1e4a8d471f1d36db87c59c3756
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539667"
---
# <a name="xrbias-color-channel-conversion-rules"></a>XR\_バイアス カラー チャネルの変換規則


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

これらのトピックが XR 間の変換の要件を満たすため\_バイアス、およびその他の色チャネル。

[XR\_変換規則のフローティング バイアス](xr-bias-to-float-conversion-rules.md)

[XR に寄せて配置\_バイアス変換規則](float-to-xr-bias-conversion-rules.md)

[BGR8888 から XR への変換\_バイアス](conversion-from-bgr8888-to-xr-bias.md)

いくつかの変換規則を使用して値の変換例を次に示します。

| フレーム バッファー値 | 意味 |
|--------------------|----------------|
| 000 = 0x000        | -0.7529        |
| 129 = 0x081        | -0.5000        |
| 384 = 0x180        | 0.0000         |
| 639 = 0x27f        | 0.5000         |
| 894 = 0x37e        | 1.0000         |
| 1023 = 0x3ff       | 1.2529         |

 

 

 





