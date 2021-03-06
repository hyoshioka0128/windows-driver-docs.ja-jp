---
title: GPIO 割り込みマスク
description: 割り込み入力はマスクやほかにマスク解除が有効と無効にできるように構成されている汎用の I/O (GPIO) ピンです。
ms.assetid: FD6537DA-2AAA-4646-896D-D5BC834526B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6e0e04a2a6dc3741bf168f267f4fce59175af8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383417"
---
# <a name="gpio-interrupt-masks"></a>GPIO 割り込みマスク


割り込み入力はマスクやほかにマスク解除が有効と無効にできるように構成されている汎用の I/O (GPIO) ピンです。

ハンドラーが、暗証番号 (pin) を防ぐために GPIO ピンの割り込みをマスクの周辺機器からレベルによってトリガーされる割り込みが有効化され、アクティブな場合、カーネルのトラップ ハンドラーは、デバイスの割り込みサービス ルーチン (ISR) を割り込みをオフにすぐに実行ことはできません。繰り返し割り込みが発生します。 後で、ISR で動作し、割り込みをクリアした後、割り込みできますマスク解除する安全にします。

割り込みのマスクをオフにしたりしない、割り込みを無効にします。 GPIO 割り込みが有効になっている場合、unmasking active、マスクされたこの割り込みにより GPIO コント ローラー デバイスからプロセッサに割り込み要求を通知します。

GPIO 割り込みが無効になっているときに、GPIO 割り込みマスクのビットを指定しても効果はありません。 [*クライアント\_EnableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)コールバック関数はビットを 0 に割り込みをマスクを設定します。 これは、割り込みが最初にマスクされていないが有効になる場合。

マスクと割り込み GPIO ピンを無効化の重要な違いは、マスクがピンの割り込み構成設定を保存する、pin を無効化は実行されません。 割り込み GPIO ピンがマスクされており、中に、以前下手順の割り込みのモード (edge によってトリガーされるまたはレベルによってトリガーされる) 極性 (アクティブ-高、アクティブ-低、またはアクティブ両方) を保持および debounce 設定します。 割り込みがマスクされていないとすぐには、もう一度有効にこれらの設定。 ただし、割り込みを無効にすると、すべてのピンの割り込み構成設定は失われます。 Pin が有効にした後は、必要な割り込み構成設定でもう一度、プログラミングする必要があります。

一部の GPIO コント ローラーを実装、ハードウェアでは別個の割り込みを有効にレジスタから割り込みマスク レジスタ。

ただし、他の GPIO コント ローラーは、割り込みマスクと割り込みを有効に機能を組み合わせるハードウェア レジスタの 1 つのセットを提供します。 これらのコント ローラーのドライバーでは、ソフトウェアで個別の割り込みマスクと割り込みを有効にレジスタをエミュレートします。 これを行うには、これらのドライバーが割り込み有効ビット、割り込みマスクのビットの論理状態を追跡し、結合論理の割り込みの有効化と割り込みマスクの動作を正確に反映するように、ハードウェア レジスタに対応するビットを操作各 GPIO 割り込みのビットです。

 

 




