---
title: 仮想マシンキュー (VMQ) の概要
description: 仮想マシンキュー (VMQ) の概要
ms.assetid: c502c7d6-bdf1-4656-b5a5-339250910f08
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 303376a8c5bdfae7e44a8e62798ec90f5153a50b
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565728"
---
# <a name="virtual-machine-queue-vmq-overview"></a>仮想マシンキュー (VMQ) の概要

このセクションでは、NDIS virtual machine queue (VMQ) インターフェイスについて説明します。 VMQ インターフェイスでは、Windows Server 2008 R2 以降のバージョンの Windows Server で、Microsoft Hyper-v ネットワークパフォーマンス6.20 の向上がサポートされています。

[仮想マシンキューアーキテクチャ](virtual-machine-queue-architecture.md)のドキュメントでは、VMQ アーキテクチャの概要について説明します。 [Vmq ドライバーの記述](writing-vmq-drivers.md)に関するドキュメントには、NDIS VMQ ドライバーの記述に関する詳細情報が記載されています。

注   [NDIS 仮想ミニポートドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617918)(特に、vmq と vmq のソースファイル) を確認してください。

 

VMQ インターフェイスでは、次の機能がサポートされます。

-   宛先メディアアクセス制御 (MAC) アドレスを使用してパケットを別の受信キューにルーティングすることによって、ネットワークアダプターハードウェアで受信したパケットの分類。

-   NIC は、DMA を使用して、仮想マシンの共有メモリにパケットを直接転送できます。 共有メモリの詳細については、「 [NDIS Memory Management Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)」を参照してください。

-   異なるプロセッサ上の異なる仮想マシンのパケットを処理することにより、複数のプロセッサにスケーリングします。

ここでは、次のトピックについて説明します。

-   [仮想マシンキューアーキテクチャ](virtual-machine-queue-architecture.md)
-   [VMQ ドライバーの記述](writing-vmq-drivers.md)