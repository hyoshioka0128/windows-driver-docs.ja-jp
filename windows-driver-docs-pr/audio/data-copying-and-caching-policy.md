---
title: データのコピーおよびキャッシュのポリシー
description: データのコピーおよびキャッシュのポリシー
ms.assetid: 1867f2bd-240c-4525-9f02-98b8f1d54b17
keywords:
- HD オーディオ、キャッシュ
- High Definition Audio (HD audio), キャッシュ
- WDK オーディオをキャッシュする
- バススヌーピング WDK audio
- WDK オーディオの覗き見
- メモリ WDK オーディオ
- オーディオデータのコピー
- WDK オーディオのデータコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4449e4328b31b23eec5ca6086ae3974fcab6af28
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925611"
---
# <a name="data-copying-and-caching-policy"></a>データのコピーおよびキャッシュのポリシー


WaveCyclic ミニポートドライバーは、HD audio controller ハードウェアがアクセスする DMA バッファーと、ユーザーモードオーディオアプリケーションがアクセスするクライアントバッファーとの間でオーディオデータをコピーします。

-   再生データストリームの場合、ドライバーはクライアントバッファーから DMA バッファーにデータをコピーします。

-   キャプチャデータストリームの場合、ドライバーは DMA バッファーからクライアントバッファーにデータをコピーします。

再生ストリームとキャプチャストリームの両方で、ドライバーは DMA バッファーメモリ (キャッシュの種類**Mmcached**) のキャッシュを有効にし、PCI コントローラーのバススヌーピングメカニズムに依存してキャッシュの一貫性を確保することで、最高のパフォーマンスを実現できます。 ただし、一部の PCI Express コントローラーの実装では、HD オーディオコントローラーのアイソクロナスデータ転送 (Intel の初期 PCI Express チップセットなど) が snoop されることはありません。

関数ドライバーは、PCI コントローラーハードウェアが DMA バッファー転送の覗き見をサポートするか、またはアイソクロナスデータ転送を実行するかを検出できません。 キャッシュの一貫性の問題の可能性を回避するために、ドライバーは、そのメモリのキャッシュの種類を**Mmwritecombined**として指定することにより、DMA バッファーメモリのキャッシュを無効にします。 (**Mmnoncached**も機能しますが、同様に実行することはできません)。サンプル関数ドライバーに基づくカスタムアダプタードライバーを記述する場合、WaveCyclic ミニポートドライバーは、実際に PCI コントローラーが DMA バッファー転送の覗き見をサポートしているかどうかを確認できない限り、同じように動作します。

バスの覗き見を実行しないデバイスとシステムをサポートするには、カスタム関数ドライバーが次の規則に従う必要があります。

-   再生ストリームの場合は、DMA バッファーのキャッシュの種類を**Mmwritecombined**として指定します。 クライアントバッファーから DMA バッファーにデータのブロックをコピーしたら、 [**KeMemoryBarrier**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kememorybarrier)関数を呼び出して、データが dma エンジンに表示されるようにします。 **KeMemoryBarrier**は、コピーされたデータを効率的な方法でメモリにフラッシュします。これにより、プロセッサのデータキャッシュはほとんど変わりません。

-   キャプチャストリームの場合、DMA バッファーのキャッシュの種類として**Mmwritecombined**または**mmnoncached**を指定します。 また、関数ドライバーは DMA バッファーへの書き込みを回避する必要があります。 オーディオサンプルのインプレース処理を実行する必要がある場合は、まずデータを別の場所にコピーする必要があります。

関数ドライバーが DMA バッファーとの間でコピーを行うデータのブロックは、書き込み結合バッファー境界で開始または終了する必要はありません。また、サイズは書き込み結合バッファーサイズの倍数 (通常は32または64バイト) である必要はありません。

[**Hdaudio\_BUS\_インターフェイス\_bdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)バージョンの DDI を使用するコーデック関数ドライバーの場合、 [**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)ルーチンは DMA バッファーメモリの割り当てとマッピングの両方を実行します。 このルーチンは常に、バッファーのキャッシュの種類を**Mmwritecombined**に設定します。

書き込み結合の詳細については、 [intel](https://www.intel.com/content/www/us/en/homepage.html)の web サイトにある IA-32 Intel Architecture Software Developer'S のマニュアルを参照してください。

 

 




