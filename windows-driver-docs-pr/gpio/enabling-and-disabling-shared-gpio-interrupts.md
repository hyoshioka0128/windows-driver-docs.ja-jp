---
title: 共有 GPIO 割り込みの有効化と無効化
description: 場合によっては、2つ以上の周辺機器からの割り込み要求行が、同じ物理汎用 i/o (GPIO) ピンに接続することがあります。 共有割り込み線の GPIO ピンは、通常、レベルでトリガーされる割り込み用に構成されます。
ms.assetid: F3C8F2B1-54BC-46A1-8AC2-50006E1156FF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a22c86b1d31edb2cc121941c3024a3278b615df3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825047"
---
# <a name="enabling-and-disabling-shared-gpio-interrupts"></a>共有 GPIO 割り込みの有効化と無効化


場合によっては、2つ以上の周辺機器からの割り込み要求行が、同じ物理汎用 i/o (GPIO) ピンに接続することがあります。 共有割り込み線の GPIO ピンは、通常、レベルでトリガーされる割り込み用に構成されます。

これらのデバイスのドライバーが、この GPIO ピンで割り込みがアサートされたときにトリガーされるように割り込みサービスルーチン (Isr) を登録する場合、GPIO framework 拡張機能 (GpioClx) は、[*クライアント\_EnableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt) callback 関数を呼び出します。最初のドライバーは、この割り込みを登録します。 他のドライバーが既に有効になっている GPIO 割り込みを使用するように登録すると、GpioClx はこれらの登録を内部で追跡しますが、この割り込みを有効にするために、*クライアント\_EnableInterrupt* callback 関数を冗長に呼び出します。 同様に、GpioClx は、登録されているこれらのドライバーの最後に割り込みが解放された場合にのみ、[*クライアント\_DisableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) callback 関数を呼び出します。

 

 




