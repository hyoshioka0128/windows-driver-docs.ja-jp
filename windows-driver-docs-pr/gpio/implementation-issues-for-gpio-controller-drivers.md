---
title: GPIO コントローラー ドライバーの実装上の問題
description: GPIO フレームワーク拡張機能 (GpioClx) は、柔軟性に優れたデバイス ドライバー インターフェイス (DDI) を提供します。
ms.assetid: 303A6034-7ED7-4C21-86E5-076383AF3A5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c3db49ee9d007272ba8cc0dcc7f44a45039d302
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363585"
---
# <a name="implementation-issues-for-gpio-controller-drivers"></a>GPIO コントローラー ドライバーの実装上の問題


GPIO フレームワーク拡張機能 (GpioClx) は、柔軟性に優れたデバイス ドライバー インターフェイス (DDI) を提供します。 この DDI では、代替のコールバック インターフェイスを選択することができます。 ドライバー開発者は、ターゲットの GPIO コント ローラー デバイスのハードウェア アーキテクチャに最適であるイベントのコールバック関数のセットを実装する必要があります。

たとえばからの読み取りと書き込み I/O の GPIO ピンを GPIO コント ローラー用ドライバーをサポートする場合、開発者は次のコールバック関数のペアの 1 つを実装するために選択できます。

[*クライアント\_ReadGpioPins* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins)と[*クライアント\_WriteGpioPins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins)
[*クライアント\_ReadGpioPinsUsingMask* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)と[*クライアント\_WriteGpioPinsUsingMask* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_write_pins_mask) 、*クライアント\_ReadGpioPins*と*クライアント\_WriteGpioPins*関数受信銀行番号、GPIO ピンの数値の配列、およびビット値のデータ バッファーから読み取りまたはこれらのピンに書き込まれます。 GPIO ピンの数が少ないは通常、読み取りまたは書き込み操作のアクセス、だけの場合、この 2 つのコールバックは、最適な実装を生じる可能性があります。 この実装が使用される通常の GPIO コント ローラーがハードウェアの登録がないメモリ マップトします。 ただし、いくつかの GPIO ピンが書き込み操作、または読み取り中にアクセスする可能性がある場合、または GPIO コント ローラーのハードウェアが並列で複数の GPIO ピンを効率的にアクセスできる場合は、他の 2 つのコールバック関数は、実装を生成可能性があります。

*クライアント\_ReadGpioPinsUsingMask*と*クライアント\_WriteGpioPinsUsingMask*コールバック関数が読み取りまたは 1 回の呼び出しで最大 64 個のピンの銀行を記述します。 *クライアント\_ReadGpioPinsUsingMask*関数は、64 ビット マスクに GPIO ピンの値を読み取ります。 *クライアント\_WriteGpioPinsUsingMask*関数は 2 つの 64 ビット マスクを使用します。 1 つのマスクを設定するには、どの GPIO ピンを示し、その他のマスクは、GPIO ピンをオフにすることを示します。 この実装は、メモリ マップト GPIO コント ローラーの通常使用されます。

 

 




