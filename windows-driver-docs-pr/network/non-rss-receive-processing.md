---
title: 非 RSS 受信処理
description: 非 RSS 受信処理
ms.assetid: 9fe262c3-9ce5-4625-8d29-ff7dc4ccb90a
keywords:
- 受信側のスケーリング WDK ネットワーク、RSS 以外の受信処理
- RSS WDK ネットワーク、RSS 以外の受信処理
- RSS 以外の受信処理 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 176e41c7c2df6e5f68e7a6e7dd1799bd5120b40a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842769"
---
# <a name="non-rss-receive-processing"></a>非 RSS 受信処理





このトピックで説明されているように、RSS ハンドル受信処理をサポートしないミニポートドライバー。

次の図は、RSS 以外の受信処理を示しています。

![rss を使用しない送信処理と受信処理を示す図](images/rsslessstack.png)

この図では、破線パスは送信処理と受信処理の代替パスを表しています。 システムではスケーリングが制御されるため、最適なパフォーマンスを提供する CPU 上では常に処理が行われるわけではありません。 接続は、確率によってのみ、連続した割り込みで同じ CPU で処理されます。

次のプロセスは、RSS 以外の割り込みサイクルごとに繰り返されます。

1.  NIC は DMA を使用して、受信したデータをバッファーに格納し、システムに割り込みます。

    ミニポートドライバーは、初期化中に共有メモリ内に受信バッファーを割り当てていました。

2.  NIC は、この割り込みサイクルでいつでも追加の受信バッファーを使用できます。 ただし、ミニポートドライバーで割り込みが有効になるまで、NIC は再び中断しません。

    1つの割り込みサイクルでシステムが処理する受信バッファーは、さまざまなネットワーク接続に関連付けることができます。

3.  NDIS は、システムによって決定された CPU でミニポートドライバーの[*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数 (ISR) を呼び出します。

    理想的には、ISR は最も負荷の低い CPU にアクセスする必要があります。 ただし、システムによっては、使用可能な CPU または NIC に関連付けられている CPU に ISR が割り当てられます。

4.  ISR は割り込みを無効にし、受信したデータを処理するために遅延プロシージャ呼び出し (DPC) をキューに送信するように NDIS に要求します。

5.  NDIS は、現在の CPU で[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)関数 (DPC) を呼び出します。

6.  DPC は、受信したすべてのバッファーの受信記述子を作成し、ドライバースタックのデータを示します。 詳細については、「[ネットワークデータの受信](receiving-network-data.md)」を参照してください。

    多くの異なる接続に対して多くのバッファーが存在し、処理が大量に完了する可能性があります。 後続の割り込みサイクルに関連付けられている受信データは、他の Cpu で処理できます。 また、特定のネットワーク接続の送信処理は、別の CPU でも実行できます。

7.  DPC によって割り込みが有効になります。 この割り込みサイクルは完了し、プロセスは再び開始されます。

 

 





