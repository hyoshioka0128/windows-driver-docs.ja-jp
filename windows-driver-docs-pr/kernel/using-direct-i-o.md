---
title: ダイレクト I/O を使用します。
description: ダイレクト I/O を使用します。
ms.assetid: e40b4657-833f-404c-8472-2e33564129a5
keywords:
- ダイレクト I/O WDK カーネル
- WDK の I/O バッファーのダイレクト I/O
- データ バッファーの WDK I/O、ダイレクト I/O
- I/O WDK カーネルでは、ダイレクト I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68bb773f5ab4b8c62667ca2b57b0cff190b91814
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531703"
---
# <a name="using-direct-io"></a>ダイレクト I/O を使用します。





一度に大量のデータを転送できるデバイスのドライバーでは、これらの転送のダイレクト I/O を使用してください。 サイズの大きな転送ダイレクト I/O を使用すると、その割り込みオーバーヘッドを減らすことでと、メモリの割り当てを排除し、バッファー内の I/O に固有の操作をコピーして、ドライバーのパフォーマンスが向上します。

一般に、大容量記憶装置のドライバーが要求はダイレクト メモリ アクセス (DMA) を使用して、または I/O (PIO) をプログラミングする最下位レベルのドライバーの上にチェーンされているすべての中間ドライバーなど、転送要求の I/O を指示します。

I/O マネージャーは、I/O 操作がダイレクト I/O を次のように使用することを決定します。

-   [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)操作を要求します。\_直接\_IO が設定されている、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)構造体。 詳細については、次を参照してください。[デバイス オブジェクトを初期化して](initializing-a-device-object.md)します。

-   [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)要求、IOCTL コードの値には、メソッドが含まれています\_IN\_ダイレクトまたはメソッド\_アウト\_、として直接 *。TransferType* IOCTL 値の値。 詳細については、次を参照してください。 [I/O 制御コードを定義する](defining-i-o-control-codes.md)します。

ダイレクト I/O を使用するドライバーでは、一部の Irp の処理にバッファー内の I/O を使用することもあります。 具体的には、ドライバー通常を使用して、バッファー内の I/O のいくつか I/O 制御コードの**IRP\_MJ\_デバイス\_コントロール**ドライバーを使用するかどうかに関係なく、データ転送を必要とする要求ダイレクト I/O による読み取りおよび書き込み操作。

I/O を直接転送の設定は、DMA または PIO を使用するかどうかによって多少異なります。 詳しくは、次のトピックをご覧ください。

[DMA でのダイレクト I/O の使用](using-direct-i-o-with-dma.md)

[ダイレクト I/O PIO の併用](using-direct-i-o-with-pio.md)

ドライバーは、DMA および PIO 転送中にキャッシュの一貫性を維持するために手順を実行する必要があります。 詳細については、次を参照してください。[キャッシュの一貫性を維持](maintaining-cache-coherency.md)します。

 

 




