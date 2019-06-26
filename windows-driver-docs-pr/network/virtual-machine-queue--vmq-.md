---
title: 仮想マシン キュー (VMQ)
description: 仮想マシン キュー (VMQ)
ms.assetid: c502c7d6-bdf1-4656-b5a5-339250910f08
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 285e8d2e07bf8519ab13fff81a5759a6f9698108
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353638"
---
# <a name="virtual-machine-queue-vmq"></a>仮想マシン キュー (VMQ)





このセクションでは、NDIS 仮想マシン キュー (VMQ) インターフェイスについて説明します。 VMQ インターフェイスは、NDIS 6.20 が動作では Windows Server 2008 R2 およびそれ以降のバージョンの Windows Server に後で、Microsoft、HYPER-V ネットワーク パフォーマンスの向上をサポートしています。

[仮想マシン キュー アーキテクチャ](virtual-machine-queue-architecture.md)VMQ アーキテクチャの大まかな概念について説明します。 [VMQ ドライバーの記述](writing-vmq-drivers.md)ドキュメントは VMQ の NDIS ドライバーの開発についてより詳細な情報を提供します。

**注**  学習してください、 [NDIS 仮想ミニポート ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617918)、特に vmq.c と vmq.h ソース ファイル。

 

VMQ インターフェイスをサポートします。

-   分類別に、パケットをルーティングする先のメディア アクセス制御 (MAC) アドレスを使用して、ネットワーク アダプターのハードウェアで受信したパケットのキューが表示されます。

-   DMA を使用して仮想マシンに直接パケットを転送する NIC 機能は、メモリを共有します。 共有メモリの詳細については、次を参照してください。 [NDIS メモリ管理インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

-   異なるプロセッサ上の別の仮想マシンのパケットを処理することによって、複数のプロセッサをスケーリングします。

ここでは、次のトピックについて説明します。

-   [仮想マシン キューのアーキテクチャ](virtual-machine-queue-architecture.md)
-   [書き込み VMQ ドライバー](writing-vmq-drivers.md)

 

 





