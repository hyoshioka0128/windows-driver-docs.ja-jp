---
title: IEEE 1394 デバイス バッファリング アイソクロナス DMA 転送
description: IEEE 1394 デバイス バッファリング アイソクロナス DMA 転送
ms.assetid: 5a08303b-8a4a-4c55-ba48-c4d5ea06157e
keywords:
- DMA をバッファリング アイソクロナスの I/O WDK の IEEE 1394 bus 転送します。
- WDK の IEEE 1394 をバッファー処理します。
- DMA が IEEE 1394 の WDK を転送します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c11deb2df1752d7866417537c7d8ce7e1f1660c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552187"
---
# <a name="buffering-isochronous-dma-transfers-for-ieee-1394-devices"></a>IEEE 1394 デバイス バッファリング アイソクロナス DMA 転送





開始されると、アイソクロナス転送は停止するまで継続的なです。 ホスト コント ローラーには、トランザクションの需要に対処するバッファーの準備完了の提供が必要です。 バス ドライバーは、使用されるまで、リソースのハンドルにアタッチされているバッファーを使用し、DMA が中断します。 これが発生する前に、ドライバーは、トランザクションを続行する追加のバッファーをアタッチします。 アイソクロナス\_バッファー記述子は、のバッファーを持つバス ドライバーが完了すると、コールバックを提供する必要に応じて、ドライバーは追加のバッファーをアタッチするこれを使用できます。 最適なパフォーマンスをドライバーでは、一度に複数のバッファーをアタッチし、最後のバッファーのバッファーの提供が不足することを通知するだけでコールバックを提供する必要があります。

次の図は、isochronous 転送に使用されるバッファーを示します。

![isochronous 転送に使用されるバッファーを示す図](images/1394lin.png)

 

 




