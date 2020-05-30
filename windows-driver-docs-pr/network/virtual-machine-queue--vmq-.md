---
title: 仮想マシン キュー (VMQ) の概要
description: 仮想マシン キュー (VMQ) の概要
ms.assetid: c502c7d6-bdf1-4656-b5a5-339250910f08
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: e712deaaa1d3b88a6d66e557b79dd5db67985c2f
ms.sourcegitcommit: 3de08bb83cc4150fe2bf09610c254602947499ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84205640"
---
# <a name="virtual-machine-queue-vmq-overview"></a>仮想マシン キュー (VMQ) の概要

NDIS 仮想マシンキュー (VMQ) インターフェイスでは、Windows server 2008 R2 以降のバージョンの Windows Server で、NDIS 6.20 以降の Microsoft Hyper-V ネットワークパフォーマンスの向上がサポートされています。

- [仮想マシンキューアーキテクチャ](virtual-machine-queue-architecture.md)では、VMQ アーキテクチャの概要について説明します。

- [Vmq ドライバー](writing-vmq-drivers.md)の作成に関する詳細については、「」を参照してください。

> [!NOTE]
> 必ず、 [NDIS 仮想ミニポートドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/netvmini/6x)(特に、vmq と vmq のソースファイル) を調べてください。

VMQ インターフェイスでは、次の機能がサポートされます。

- 宛先メディアアクセス制御 (MAC) アドレスを使用してパケットを別の受信キューにルーティングすることによって、ネットワークアダプターハードウェアで受信したパケットの分類。

- 共有メモリ;詳細については、「 [NDIS Memory Management Interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

- 異なるプロセッサ上の異なる仮想マシンのパケットを処理することにより、複数のプロセッサにスケーリングします。

## <a name="related-topics"></a>関連トピック

- [仮想マシン キュー アーキテクチャ](virtual-machine-queue-architecture.md)
- [VMQ ドライバーの作成](writing-vmq-drivers.md)
