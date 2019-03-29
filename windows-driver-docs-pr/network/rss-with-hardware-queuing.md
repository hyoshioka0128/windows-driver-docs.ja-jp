---
title: ハードウェア キューを使用した RSS
description: ハードウェア キューを使用した RSS
ms.assetid: f37caef9-6d22-4d17-8628-0c3f93de470e
keywords:
- 受信側のスケーリング、WDK のネットワーク ハードウェア キュー
- ネットワーク、RSS WDK ハードウェア キュー
- ハードウェアの WDK RSS のキュー
- WDK RSS のキューの受信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3120c2ad34d3d818a90b109ed56d0d730e76631c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581199"
---
# <a name="rss-with-hardware-queuing"></a>ハードウェア キューを使用した RSS





ハードウェア キューで RSS 向上システム RSS の基準とした 1 つのハードウェアでのパフォーマンスは、キューのソリューションを受信します。 Nic がサポート ハードウェア キュー受信した割り当てデータを複数受信キューであること。 受信キューでは、CPU に関連付けられます。 NIC は、ハッシュ値と、間接指定テーブルに基づいて Cpu に受信したデータを割り当てます。

次の図は、NIC で RSS キューを受信します。

![nic の図の示す rss の受信キュー](images/rssqstack.png)

図では、破線の矢印は、受信処理のための代替パスを表します。 RSS は、ISR の最初の呼び出しを受信する CPU を制御できません。 ドライバーは、適切な Cpu で初期 Dpc を直ちにスケジュールすることができますので、データをキューにはありません。

各割り込みに対する次のプロセスが繰り返されます。

1.  NIC:
    1.  DMA を使用して、受信したデータをバッファーに入力します。

        ミニポート ドライバーでは、初期化中に、受信バッファーを共有メモリが割り当てられます。

    2.  ハッシュ値を計算します。
    3.  バッファー、CPU のキューに配置し、ミニポート ドライバーにキューの割り当てを提供します。

        たとえば、NIC がいくつかのパケットが受信した後、手順 1-3 と DMA CPU 割り当ての一覧をループでした。 特定のメカニズムは、NIC の設計にままです。

    4.  システムが中断されます。

        1 つの割り込みでシステムを処理する受信バッファーは、Cpu 間で分散されます。

2.  NDIS ミニポート ドライバーの呼び出す[ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)関数 (ISR) システムで決定された CPU にします。

3.  ミニポート ドライバーでは、NDIS に空でないキューを作成する Cpu ごとの遅延プロシージャ呼び出し (Dpc) のキューに登録を要求します。

    すべての Dpc がドライバー割り込みを有効にする前に完了する必要があることに注意してください。 また、ISR を処理するバッファーを持たない CPU で実行できることに注意してください。

4.  NDIS 呼び出し、 [ *MiniportInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559398)の DPC キューごとに機能します。 特定の CPU で DPC:
    1.  ビルドでは、そのキュー内のすべての受信バッファー記述子を受信し、ドライバー スタック上のデータを示します。

        詳細については、次を参照してください。 [RSS の受信データのことを示す](indicating-rss-receive-data.md)します。

    2.  完了する最後の DPC にある場合は、割り込みを有効にします。 この割り込みが完了し、プロセスが再び開始します。 ドライバーは、分割不可能な操作を完了するのに最後の DPC を識別するために使用する必要があります。 たとえば、ドライバーを使用できます、 [ **NdisInterlockedDecrement** ](https://msdn.microsoft.com/library/windows/hardware/ff562751)アトミックのカウンターを実装する関数。

 

 





