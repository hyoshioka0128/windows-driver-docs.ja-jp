---
title: ハードウェア キューを使用した RSS
description: ハードウェア キューを使用した RSS
ms.assetid: f37caef9-6d22-4d17-8628-0c3f93de470e
keywords:
- 受信側のスケーリング WDK ネットワーク、ハードウェアキュー
- RSS WDK ネットワーク, ハードウェアキュー
- ハードウェアキュー WDK RSS
- 受信キュー WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b7fed29d69f0d321b1df05d9fed1a79443becc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841998"
---
# <a name="rss-with-hardware-queuing"></a>ハードウェア キューを使用した RSS





ハードウェアキューを使用する RSS では、ハードウェア受信キューソリューションが1つの RSS と比べて、システムのパフォーマンスが向上します。 ハードウェアキューをサポートする Nic は、受信したデータを複数の受信キューに割り当てます。 Receive キューは CPU に関連付けられています。 NIC は、ハッシュ値と間接テーブルに基づいて、受信したデータを Cpu に割り当てます。

次の図は、NIC 受信キューの RSS を示しています。

![nic 受信キューを使用した rss を示す図](images/rssqstack.png)

この図では、破線の矢印は受信処理の代替パスを表しています。 RSS は、最初の ISR 呼び出しを受け取る CPU を制御できません。 ドライバーは、正しい Cpu の初期 Dpc を直ちにスケジュールできるように、データをキューに入れている必要はありません。

割り込みごとに次のプロセスが繰り返されます。

1.  NIC:
    1.  は DMA を使用して、受信したデータをバッファーに格納します。

        ミニポートドライバーは、初期化中に共有メモリ内に受信バッファーを割り当てていました。

    2.  ハッシュ値を計算します。
    3.  CPU のバッファーをキューに格納し、ミニポートドライバーにキュー割り当てを提供します。

        たとえば、NIC は、いくつかのパケットを受信した後に、手順1-3 と DMA の CPU 割り当ての一覧をループすることがあります。 NIC の設計には、特定のメカニズムが残されています。

    4.  システムを中断します。

        1つの割り込みでシステムが処理する受信バッファーは、Cpu 間に分散されます。

2.  NDIS は、システムによって決定された CPU でミニポートドライバーの[*Miniportinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)関数 (ISR) を呼び出します。

3.  ミニポートドライバーは、空でないキューを持つ Cpu ごとに、遅延プロシージャ呼び出し (Dpc) をキューに要求します。

    ドライバーで割り込みが有効になる前に、すべての Dpc が完了する必要があることに注意してください。 また、ISR は処理するバッファーがない CPU 上で実行されている可能性があることに注意してください。

4.  NDIS は、キューに置かれている DPC ごとに[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)関数を呼び出します。 特定の CPU 上の DPC:
    1.  キュー内の受信したすべてのバッファーの受信記述子をビルドし、ドライバースタックのデータを示します。

        詳細については、「 [RSS 受信データの表示](indicating-rss-receive-data.md)」を参照してください。

    2.  最後の DPC が完了すると、割り込みを有効にします。 この割り込みは完了し、プロセスは再び開始されます。 ドライバーは、完了する最後の DPC を識別するためにアトミック操作を使用する必要があります。 たとえば、ドライバーは[**NdisInterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockeddecrement)関数を使用して atomic カウンターを実装できます。

 

 





