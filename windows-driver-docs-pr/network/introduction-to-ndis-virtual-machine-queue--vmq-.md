---
title: NDIS 仮想マシン キュー (VMQ) の概要
description: NDIS 仮想マシン キュー (VMQ) の概要
ms.assetid: 03c6bbd1-bd4f-415f-b4ed-c6e812c50f8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5aad0b79cf7eb6ca1d3d468b6908270a4b1d6b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329883"
---
# <a name="introduction-to-ndis-virtual-machine-queue-vmq"></a>NDIS 仮想マシン キュー (VMQ) の概要





多くのネットワーク アダプターでは、ネットワーク サーバーを 1 つ以上のユニキャスト メディア アクセス制御 (MAC) アドレスをサポートできます。 そのため、ネットワーク アダプターでは、ネットワークのデータ フレームを転送先の無作為検出モードでないネットワーク アダプターのハードウェアに設定されている、ユニキャスト MAC アドレスのいずれかに一致する MAC アドレスを受信できます。 このようなハードウェアでは、各 MAC アドレスの受信キューを割り当てるでき、一致する MAC アドレスを持つ受信フレームをキューにルーティングすることができます。 割り当てる機能と組み合わせると、この機能は、各仮想マシンに割り当てられている、VMQ のサポートを必要とされる主な機能は、メモリ アドレス空間からキューごとにバッファーを受信します。

VMQ 対応のネットワーク アダプターでは、DMA を使用して、そのキューに割り当てられている受信バッファーへの受信キューにルーティングする必要があるすべての着信フレームを転送します。 ミニポート ドライバーには、すべての受信を示す値の 1 つの呼び出しで受信キューに入っているフレームを指定できます。

VMQ には、次の機能が用意されています。

-   複数のプロセッサ間で複数の仮想マシン (Vm) のネットワーク トラフィックの処理を分散することによってネットワーク スループットが向上します。

    **注**  で、HYPER-V 子パーティションは、VM でとも呼ばれます。

     

-   CPU の削減オフロードの使用率の受信パケットのネットワーク アダプターのハードウェアにフィルタ リングします。

-   DMA を使用して VM のメモリに直接データを転送するには、ネットワーク データのコピーを防止します。

-   セキュリティで保護された環境を提供するネットワークのデータを分割します。 セキュリティの問題に関する詳細については、次を参照してください。 [NDIS 仮想マシン (VM) の共有メモリのセキュリティ問題に](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)します。

    **注**  NDIS 6.30 および Windows Server 2012 以降、ネットワーク データを別の lookahead バッファーに分割することは現在サポートされていません。

     

-   ライブ マイグレーションできます。 ライブ マイグレーションの詳細については、次を参照してください。 [NDIS VMQ ライブ マイグレーションをサポート](ndis-vmq-live-migration-support.md)します。

VMQ の高度な概念を紹介するには、このセクションには、次の補足トピックが含まれます。

[VMQ コンポーネント](vmq-components.md)

[VMQ キューを受信します。](vmq-receive-queues.md)

[VMQ 受信フィルター](vmq-receive-filters.md)

 

 





