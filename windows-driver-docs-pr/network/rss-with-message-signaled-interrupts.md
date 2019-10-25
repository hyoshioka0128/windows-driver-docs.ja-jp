---
title: メッセージ シグナル割り込みを使用した RSS
description: メッセージ シグナル割り込みを使用した RSS
ms.assetid: 3c1776cf-f870-4910-88b2-9b5a9544cdf8
keywords:
- 受信側のスケーリング WDK ネットワーク、メッセージシグナル割り込み
- RSS WDK ネットワーク、メッセージシグナル割り込み
- メッセージシグナル割り込み、WDK ネットワーク、RSS
- Msi WDK ネットワーク、RSS
- MSI-X WDK ネットワーク、RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ba5edc1822a63ddbdb50785a1eb457bc90a2d43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841996"
---
# <a name="rss-with-message-signaled-interrupts"></a>メッセージ シグナル割り込みを使用した RSS





ミニポートドライバーは、RSS のパフォーマンスを向上させるために、メッセージシグナル割り込み (Msi) をサポートできます。 Msi は、受信したデータを処理する CPU の割り込みを NIC が要求できるようにします。 MSI の NDIS サポートの詳細については、「 [NDIS MSI-X](ndis-msi-x.md)」を参照してください。

次の図は、MSI-X の RSS を示しています。

![msi を使用した rss を示す図-x](images/rssmsistack.png)

この図では、破線の矢印は別の接続での処理を表しています。 MSI で RSS を使用すると、NIC は接続のために正しい CPU を中断できます。

割り込みごとに次のプロセスが繰り返されます。

1.  NIC:
    1.  は DMA を使用して、受信したデータをバッファーに格納します。

        ミニポートドライバーは、初期化中に共有メモリ内に受信バッファーを割り当てていました。

    2.  ハッシュ値を計算します。
    3.  バッファーを CPU に対してキューに格納し、ミニポートドライバーにキュー割り当てを提供します。 たとえば、NIC は、いくつかのパケットを受信した後に、手順1-3 と DMA の CPU 割り当ての一覧をループすることがあります。 NIC の設計には、特定のメカニズムが残されています。
    4.  MSI-X を使用すると、空でないキューに関連付けられている CPU に割り込みます。

2.  NIC は、追加の受信バッファーを入力し、いつでもキューに追加できますが、ミニポートドライバーによってその CPU の割り込みが有効になるまで、CPU を中断しません。

3.  NDIS は、現在の CPU 上でミニポートドライバーの ISR ( [*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)) を呼び出します。

4.  ISR は、現在の CPU 上の割り込みを無効にし、現在の CPU で DPC をキューに入れます。

    割り込みは、現在の CPU で DPC が実行されている間、他の Cpu でも発生する可能性があります。

5.  NDIS は、キューに置かれている DPC ごとに[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)関数を呼び出します。 各 DPC:
    1.  キュー内の受信したすべてのバッファーの受信記述子をビルドし、ドライバースタックのデータを示します。 詳細については、「 [RSS 受信データの表示](indicating-rss-receive-data.md)」を参照してください。
    2.  現在の CPU の割り込みを有効にします。 この割り込みは完了し、プロセスは再び開始されます。 他の Dpc の進行状況を追跡するためにアトミック操作は必要ないことに注意してください。

 

 





