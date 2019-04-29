---
title: 共有 GPIO 割り込みの有効化と無効化
description: 場合によっては、2 つ以上の周辺機器からの割り込み要求行が同じ物理汎用入出力 (GPIO) ピンに接続します。 共有の割り込みの行の GPIO ピンは通常、割り込みのトリガーされたレベルの構成します。
ms.assetid: F3C8F2B1-54BC-46A1-8AC2-50006E1156FF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da7b60329d7a78860c388ca909187210905abb8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326171"
---
# <a name="enabling-and-disabling-shared-gpio-interrupts"></a>共有 GPIO 割り込みの有効化と無効化


場合によっては、2 つ以上の周辺機器からの割り込み要求行が同じ物理汎用入出力 (GPIO) ピンに接続します。 共有の割り込みの行の GPIO ピンは通常、割り込みのトリガーされたレベルの構成します。

これらのデバイス ドライバーは、この GPIO ピン GPIO フレームワークの拡張機能 (GpioClx) の呼び出しで、割り込みサービス ルーチン (Isr)、割り込みがアサートされたときにトリガーされるようを登録している場合、 [*クライアント\_EnableInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh439377)割り込みの最初のドライバーを登録する場合にのみのコールバック関数。 GpioClx が内部的にはこれらの登録を追跡しますが、冗長的呼び出されませんが、既に有効になっている GPIO 割り込みを使用するその他のドライバーを登録するときに、*クライアント\_EnableInterrupt*これを有効にするコールバック関数中断します。 同様に、GpioClx を呼び出す、 [*クライアント\_DisableInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh439371)コールバック関数の最後に、ドライバーの登録時に、割り込みをリリースのみです。

 

 




