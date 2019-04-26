---
title: パケットベース バス マスター DMA
description: パケットベース バス マスター DMA
ms.assetid: f94b9ca9-6e29-4801-a092-30af19345f6d
keywords:
- バス マスターの DMA WDK ビデオのミニポート、パケットのベース
- DMA バス マスター WDK ビデオのミニポート、パケットのベース
- パケットに基づく DMA WDK ビデオのミニポート、説明
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d352e018433c845c2d96e0ed89cd648cf6e85ec8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352418"
---
# <a name="packet-based-bus-master-dma"></a>パケットベース バス マスター DMA


## <span id="ddk_packet_based_bus_master_dma_gg"></span><span id="DDK_PACKET_BASED_BUS_MASTER_DMA_GG"></span>


通常、ディスプレイ ドライバーは、ミニポート ドライバーに譲渡要求を送信することによって、DMA 操作を開始します。 パケットに基づくの DMA 操作をサポートしているミニポート ドライバーでは、このような要求を受信したときに最初に、データ転送に関連するバッファーをロックします。 ミニポート ドライバー、ビデオ ポート ドライバーを呼び出すことによって、転送を開始します[ **VideoPortStartDma** ](https://msdn.microsoft.com/library/windows/hardware/ff570369)関数を呼び出し、ミニポート ドライバーの[ **HwVidExecuteDma** ](https://msdn.microsoft.com/library/windows/hardware/ff567330)データ転送を実行するコールバック ルーチン。 この DMA 操作は、非同期的に処理されます。**VideoPortStartDma** DMA 操作のミニポート ドライバーに制御を返すまでに完了を待機しません。

アダプターに割り当てられたシステム リソースの数と転送要求のサイズ、によって、ドライバーは可能性がありますすべての単一の DMA 操作でデータを転送できません。 ミニポート ドライバーがかどうかを確認するために返される実際の転送サイズを検査する必要がありますが、多くのデータを転送します。 ミニポート ドライバー、ビデオ ポート ドライバーを呼び出す必要があります、DMA ハードウェアには、現在の転送が完了すると、すぐ[ **VideoPortCompleteDma** ](https://msdn.microsoft.com/library/windows/hardware/ff570286)関数が現在の DMA 操作を完了します。 ミニポート ドライバーが、ビデオ ポート ドライバーの呼び出しの処理を繰り返し転送するための残存データが場合、 **VideoPortStartDma**と**VideoPortCompleteDma**繰り返し関数までの送信をこれ以上データが残ります。 すべてのデータが転送されたときに、ミニポート ドライバーには、バッファーがロックを解除する必要があります。

ミニポート ドライバーでは、次の一連のパケットに基づく DMA を使用する操作を実行します。

1.  ハードウェアの機能をシステムに報告し、アダプター オブジェクトを取得します。

    ミニポート ドライバー呼び出しビデオ ポート ドライバーの[ **VideoPortGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff570312)へのポインターを返す関数、 [**担当副社長\_DMA\_アダプター** ](https://msdn.microsoft.com/library/windows/hardware/ff570570)構造体。 通常、ミニポート ドライバーの内の初期化時にこれは、通常[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)ルーチン。 ミニポート ドライバーでは、このポインターを使用して、残りの DMA 操作。

2.  ホストのメモリをロックします。

    ミニポート ドライバー呼び出しビデオ ポート ドライバーの[ **VideoPortLockBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff570326)関数で、バッファーをプローブするには、常駐、それらのメモリ ページは、およびそれらをロックします。

3.  DMA 転送を開始します。

    ミニポート ドライバー呼び出しビデオ ポート ドライバーの[ **VideoPortStartDma** ](https://msdn.microsoft.com/library/windows/hardware/ff570369)関数で、ホスト プロセッサのメモリのフラッシュは、キャッシュ、スキャッター/ギャザー リストをビルドし、ミニポート ドライバーの呼び出し[**HwVidExecuteDma** ](https://msdn.microsoft.com/library/windows/hardware/ff567330) DMA 操作を非同期的に実行するコールバック ルーチン。 **VideoPortStartDma** DMA 操作の完了を待つことがなく、ミニポート ドライバーにコントロールを返します。

4.  DMA の転送を完了します。

    ミニポート ドライバー、ビデオ ポート ドライバーを呼び出す必要があります[ **VideoPortCompleteDma** ](https://msdn.microsoft.com/library/windows/hardware/ff570286)ハードウェア DMA 操作を終了すると、すぐに機能します。 多くのビデオ アダプターは、DMA 操作が完了すると、割り込みを生成します。 たとえば、このタイプのアダプターを持つシステムは、次のように、割り込みに対処できます。 ハードウェアは、DMA 操作が完了したミニポート ドライバーに通知する割り込みを生成するミニポート ドライバーの割り込みサービス ルーチン (ISR) を呼び出しますビデオ ポート ドライバーの[ **VideoPortQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff570339)関数呼び出しのビデオ ポート ドライバーの DPC ルーチンをキューに**VideoPortCompleteDma**関数。 ISR を直接呼び出すことはできません**VideoPortCompleteDma** IRQL ディスパッチ以下で、このビデオ ポート ドライバー関数が呼び出される必要がありますので\_レベル。

    **VideoPortCompleteDma** 、バス マスター アダプターの内部キャッシュに残っているデータをフラッシュしている未使用のリソースを解放 (によって作成されたスキャッター/ギャザーの一覧を含む**VideoPortStartDma**)。

    ミニポート ドライバーを繰り返し呼び出すを行う必要があります (たとえば、マップの使用可能なレジスタの数に制限あり) のため、データの一部が移転、もしも**VideoPortStartDma**と**VideoPortCompleteDma**まで、すべてのデータが変更されました。

5.  ホスト メモリのロックを解除します。

    すべてのデータが転送されたときに、ミニポート ドライバーは、ビデオ ポート ドライバーを呼び出す必要があります[ **VideoPortUnlockBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff570373) 2 番目の手順で取得したデータ バッファーのロックを解除します。

6.  アダプター オブジェクトを破棄します。

    *この手順は省略可能な*します。 ビデオ ポート ドライバーを呼び出すことによって、DMA アダプター オブジェクトを破棄する必要があります、何らかの理由で、ミニポート ドライバー決定した場合があるない有効期間の残りの部分の DMA 操作をさらに、 [ **VideoPortPutDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff570335)関数。

 

 





