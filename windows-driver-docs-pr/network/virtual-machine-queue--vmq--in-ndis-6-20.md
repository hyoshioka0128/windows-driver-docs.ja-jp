---
title: NDIS 6.20 が動作では、仮想マシン キュー (VMQ)
description: NDIS 6.20 が動作では、仮想マシン キュー (VMQ)
ms.assetid: fb48b019-4646-426d-b10e-d760788f9985
keywords:
- NDIS 6.20 WDK、仮想マシン キュー (VMQ)
- 仮想マシン キュー (VMQ) WDK NDIS 6.20 が動作
- VMQ WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df2443645c7ce6614b57d3eb2f25dd8880cb10b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553523"
---
# <a name="virtual-machine-queue-vmq-in-ndis-620"></a>NDIS 6.20 が動作では、仮想マシン キュー (VMQ)





NDIS 6.20 が動作には、Microsoft、HYPER-V ネットワーク パフォーマンスの向上をサポートするために仮想マシン キュー (VMQ) インターフェイスが導入されています。 NDIS 6.20 が動作し、以降のドライバーには、初期化中に VMQ 機能についての情報を提供する必要があります。 ただし、VMQ のサポートは省略可能です。

以降では、NDIS 6.20 VMQ インターフェイスをサポートします。

-   分類別に、パケットをルーティングする接続先 MAC アドレスを使用して、受信したパケットのキューが表示されます。

-   DMA を使用して HYPER-V 子パーティションに直接パケットを転送する NIC 機能は、メモリを共有します。

-   異なるプロセッサ上の別の HYPER-V パーティションのパケットを処理することによって複数のプロセッサにスケーリングします。

Microsoft、HYPER-V ネットワーク パフォーマンスの強化も chimney をサポートして、HYPER-V 子ドライバーを変更せずにパーティション。

VMQ の詳細については、[仮想マシン キュー (VMQ)](virtual-machine-queue--vmq-.md)を参照してください。

 

 





