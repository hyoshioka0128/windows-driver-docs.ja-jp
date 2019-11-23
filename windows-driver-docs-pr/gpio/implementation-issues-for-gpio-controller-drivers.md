---
title: GPIO コントローラー ドライバーの実装上の問題
description: GPIO framework 拡張機能 (GpioClx) は、柔軟なデバイスドライバーインターフェイス (DDI) を提供します。
ms.assetid: 303A6034-7ED7-4C21-86E5-076383AF3A5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39d7af056020240b3e89bacc13fcd3358a383ae2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824958"
---
# <a name="implementation-issues-for-gpio-controller-drivers"></a>GPIO コントローラー ドライバーの実装上の問題


GPIO framework 拡張機能 (GpioClx) は、柔軟なデバイスドライバーインターフェイス (DDI) を提供します。 この DDI を使用すると、開発者は別のコールバックインターフェイスを選択できます。 ドライバー開発者は、ターゲットの GPIO コントローラーデバイスのハードウェアアーキテクチャに最適な一連のイベントコールバック関数を実装する必要があります。

たとえば、gpio コントローラードライバーが GPIO i/o ピンの読み取りと書き込みをサポートしている場合、開発者は次のいずれかのコールバック関数を実装することを選択できます。

クライアント[ *\_readgpiopins*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins)および[*client\_writの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)
クライアント[ *\_ReadGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask)と[*クライアント\_WriteGpioPinsUsingMask*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask) *クライアント\_readgpiopins*および*client\_WRITEGPIOPINS*関数は、銀行番号、GPIO pin の配列、およびこれらのピンに対して読み取りまたは書き込みを行うビット値のデータバッファーを受け取ります。 読み取りまたは書き込み操作で通常アクセスされる GPIO pin の数が少ない場合は、このコールバックのペアによって最適な実装が生成される可能性があります。 この実装は、通常、ハードウェアレジスタがメモリマップトではない GPIO controller に使用されます。 ただし、読み取りまたは書き込み操作中に複数の GPIO ピンがアクセスされる可能性がある場合や、GPIO コントローラーハードウェアが複数の GPIO ピンに同時にアクセスできる場合は、他のコールバック関数のペアによって実装が改善される可能性があります。

*クライアント\_ReadGpioPinsUsingMask*と*client\_WriteGpioPinsUsingMask* callback 関数では、1回の呼び出しで最大64ピンの銀行を読み書きできます。 *クライアント\_ReadGpioPinsUsingMask*関数は、GPIO ピンの値を64ビットマスクに読み取ります。 *クライアント\_WriteGpioPinsUsingMask*関数は、2 64 ビットマスクを使用します。 1つのマスクは、どの GPIO ピンを設定するかを示し、もう一方のマスクはどの GPIO ピンをクリアするかを示します。 この実装は、通常、メモリマップトの GPIO コントローラーに使用されます。

 

 




