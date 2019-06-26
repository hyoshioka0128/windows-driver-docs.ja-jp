---
title: 単一ハードウェア受信キューを使用した RSS
description: 単一ハードウェア受信キューを使用した RSS
ms.assetid: 835f5646-4514-4973-978a-9bab0777a66c
keywords:
- 受信側のスケーリング、WDK のネットワーク ハードウェア キュー
- ネットワーク、RSS WDK ハードウェア キュー
- ハードウェアの WDK RSS のキュー
- WDK RSS のキューの受信します。
- 1 つの受信キュー WDK RSS
- 複数の受信キュー WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc9505ccdd9fffb02aea9905c75e4a4f8b40f37a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382142"
---
# <a name="rss-with-a-single-hardware-receive-queue"></a>単一ハードウェア受信キューを使用した RSS





ミニポート ドライバーは、RSS ハッシュ計算をサポートする Nic の RSS をサポートできるし、1 つの受信記述子キュー。

次の図は、RSS を 1 つの処理を示しています。 キューの記述子を受信します。

![受信記述子のキューの図の示す rss を 1 つの処理](images/rssswstack.png)

図では、破線の矢印は、受信処理のための代替パスを表します。 RSS は、ISR の最初の呼び出しを受信する CPU を制御できません。

非-RSS とは異なり、受信処理、RSS に基づく受信処理が複数の Cpu に分散します。 また、特定の接続の処理を特定の CPU に関連付けられることができます。

各割り込みに対する次のプロセスが繰り返されます。

1.  NIC は、DMA を使用して、受信したデータをバッファーに入力して、システムの割り込みです。

    ミニポート ドライバーでは、初期化中に、受信バッファーを共有メモリが割り当てられます。

2.  NIC は、追加で入力できますが、いつでも受信バッファー、ミニポート ドライバー、割り込みを有効にするまでにもう一度に中断しません。

    1 つの割り込みでシステムを処理する受信バッファーは、多くのさまざまなネットワーク接続を関連付けることができます。

3.  NDIS ミニポート ドライバーの呼び出す[ *MiniportInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)関数 (ISR) システムで決定された CPU にします。

4.  ISR には、割り込みと NDIS を要求を受信したデータの処理に遅延プロシージャ呼び出し (DPC) のキューが無効にします。

5.  NDIS 呼び出し、 [ *MiniportInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)現在の CPU に (DPC) の関数。 DPC: で

    1.  ミニポート ドライバーでは、受信バッファーの NIC が計算されたハッシュ値を使用し、CPU に関連付けられている受信キューに受信した各バッファーを再割り当ています。
    2.  現在の DPC は、NDIS ごと、その他の空の受信キューに関連付けられている Cpu の DPC をキューに登録を要求します。
    3.  現在 DPC が空でないキューに関連付けられている CPU 上で実行している場合、現在の DPC が関連付けられている受信バッファーを処理し、ドライバー スタックを受信したデータを示します。

    キューの割り当てとその他の Dpc キューには、追加の処理オーバーヘッドが必要です。 システム パフォーマンスの向上を実現するには、使用可能な Cpu 使用率の向上によってこのオーバーヘッドをオフセットする必要があります。

6.  特定の CPU で DPC:
    1.  受信キューに関連付けられている受信バッファーを処理し、ドライバー スタック上のデータを示します。 詳細については、次を参照してください。 [RSS の受信データのことを示す](indicating-rss-receive-data.md)します。
    2.  完了する最後の DPC にある場合は、割り込みを有効にします。 この割り込みが完了し、プロセスが再び開始します。 ドライバーは、分割不可能な操作を完了するのに最後の DPC を識別するために使用する必要があります。 たとえば、ドライバーを使用できます、 [ **NdisInterlockedDecrement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisinterlockeddecrement)アトミックのカウンターを実装する関数。

 

 





