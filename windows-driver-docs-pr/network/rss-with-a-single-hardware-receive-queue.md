---
title: 単一ハードウェア受信キューを使用した RSS
description: 単一ハードウェア受信キューを使用した RSS
ms.assetid: 835f5646-4514-4973-978a-9bab0777a66c
keywords:
- 受信側のスケーリング WDK ネットワーク、ハードウェアキュー
- RSS WDK ネットワーク, ハードウェアキュー
- ハードウェアキュー WDK RSS
- 受信キュー WDK RSS
- 単一の受信キュー WDK RSS
- 複数の受信キュー WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f144837af3abe9e5f40b7607d37361008367cc3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842003"
---
# <a name="rss-with-a-single-hardware-receive-queue"></a>単一ハードウェア受信キューを使用した RSS





ミニポートドライバーは、RSS ハッシュ計算と1つの受信記述子キューをサポートする Nic の RSS をサポートできます。

次の図は、1つの受信記述子キューを使用した RSS 処理を示しています。

![単一の受信記述子キューを使用した rss 処理を示す図](images/rssswstack.png)

この図では、破線の矢印は受信処理の代替パスを表しています。 RSS は、最初の ISR 呼び出しを受け取る CPU を制御できません。

RSS 以外の受信処理とは異なり、RSS ベースの受信処理は複数の Cpu に分散されます。 また、特定の接続の処理を特定の CPU に関連付けることもできます。

割り込みごとに次のプロセスが繰り返されます。

1.  NIC は DMA を使用して、受信したデータをバッファーに格納し、システムに割り込みます。

    ミニポートドライバーは、初期化中に共有メモリ内に受信バッファーを割り当てていました。

2.  NIC は、追加の受信バッファーをいつでも入力できますが、ミニポートドライバーによって割り込みが有効になるまで、もう一度中断されることはありません。

    1つの割り込みでシステムが処理する受信バッファーは、さまざまなネットワーク接続に関連付けることができます。

3.  NDIS は、システムによって決定された CPU でミニポートドライバーの[*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数 (ISR) を呼び出します。

4.  ISR は割り込みを無効にし、受信したデータを処理するために遅延プロシージャ呼び出し (DPC) をキューに送信するように NDIS に要求します。

5.  NDIS は、現在の CPU で[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)関数 (DPC) を呼び出します。 DPC:

    1.  ミニポートドライバーは、受信したバッファーごとに NIC によって計算されたハッシュ値を使用し、受信した各バッファーを CPU に関連付けられている受信キューに再割り当てします。
    2.  現在の DPC は、空でない受信キューに関連付けられている他の Cpu それぞれに対して DPC をキューに要求します。
    3.  現在の DPC が、空でないキューに関連付けられている CPU 上で実行されている場合、現在の DPC は関連付けられている受信バッファーを処理し、受信したデータをドライバースタックで取得します。

    キューを割り当て、追加の Dpc をキューに追加するには、追加の処理オーバーヘッドが必要です。 システムパフォーマンスを向上させるには、使用可能な Cpu の使用率を高めることによって、このオーバーヘッドを相殺する必要があります。

6.  特定の CPU 上の DPC:
    1.  受信キューに関連付けられている受信バッファーを処理し、ドライバースタックのデータを示します。 詳細については、「 [RSS 受信データの表示](indicating-rss-receive-data.md)」を参照してください。
    2.  最後の DPC が完了すると、割り込みを有効にします。 この割り込みは完了し、プロセスは再び開始されます。 ドライバーは、完了する最後の DPC を識別するためにアトミック操作を使用する必要があります。 たとえば、ドライバーは[**NdisInterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockeddecrement)関数を使用して atomic カウンターを実装できます。

 

 





