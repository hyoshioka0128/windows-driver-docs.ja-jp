---
title: Windows XP での PCMCIA IRQ ルーティング
description: Windows XP での PCMCIA IRQ ルーティング
ms.assetid: 9b3501ce-c536-4ec7-bb01-c449d3900fee
keywords:
- PCIC ブリッジ WDK PCMCIA バス
- PCI-PCMCIA に WDK PCMCIA のバスをブリッジします。
- IRQ ルーティング WDK PCMCIA バス
- PCMCIA WDK バス、IRQ ルーティング
- PC カード WDK PCMCIA バス
- ISA PCI への割り込み WDK PCMCIA のバスのルーティング
- PCI バスの WDK PCMCIA を中断します。
- ISA は、WDK PCMCIA のバスを中断します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e5c5f072224b59eac99aad8c84f6483373cffb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378194"
---
# <a name="pcmcia-irq-routing-on-windows-xp"></a>Windows XP での PCMCIA IRQ ルーティング





CardBus コント ローラーでサポートされている PCMCIA カードの 2 つのクラスがあります。

-   32 ビットの PCI に準拠して CardBus

-   16 ビット PC カードは、ISA のデバイスで、基本的には

CardBus カードが PCI デバイスを定義し、割り込みを管理する方法を含む、多くの点でと同様に動作します。 PCI バス上のデバイスに割り当てられている数値の範囲からそれらの IRQ 番号が割り当てられます。

16 ビット PC カードのアーキテクチャは、PCI バスよりも古いいて、これらのカードのように多数 ISA 割り込み番号を必要とします。 カードに ISA 割り込み要求 (IRQ) 番号へのアクセスがないシステムでこれらのカードを対応するために、CardBus コント ローラーのアーキテクチャが「ISA PCI への割り込みルーティングします」と呼ばれる手法の使用します。 この手法をサポートするコント ローラーは、ISA の割り込み番号を使用するように設計された 16 ビットのカードに PCI 割り込み番号を割り当てることができます。

このセクションでは、ISA PCI への割り込みのルーティングと ISA PCI への割り込みのルーティングをサポートしていない 16 ビットのカードに関連する問題について説明します。

「PCIC ブリッジ」と呼ばれる PCI-PCMCIA にブリッジを使用しているシステムはほとんど CardBus コント ローラーを考案するため、前に 16 ビット PC カードをコンピューターに接続するためにします。 これらのブリッジは CardBus のカードをサポートしていませんも ISA PCI への割り込みのルーティングをサポートしています。 そのため、このセクションの情報は、PCIC ブリッジには適用されません。

 

 





