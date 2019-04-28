---
title: PC カードの割り込みを構成するための INF オーバーライド
description: PC カードの割り込みを構成するための INF オーバーライド
ms.assetid: 90c951c4-0106-426a-b650-aeb93b893206
keywords:
- IRQ ルーティング WDK PCMCIA バス
- PCMCIA WDK バス、IRQ ルーティング
- PC カード WDK PCMCIA バス
- WDK PCMCIA のバスを中断します。
- PCI バスの WDK PCMCIA を中断します。
- ISA は、WDK PCMCIA のバスを中断します。
- INF ファイル WDK PCMCIA バス
- PcmciaExclusiveIrq
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 920d44b4cde6e909d55bddc55a9af7d0dbd0bbd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378209"
---
# <a name="inf-override-for-configuring-pc-card-interrupts"></a>PC カードの割り込みを構成するための INF オーバーライド





オペレーティング システムが共有可能な PCI 割り込みをサポートしていない 16 ビット PC カードから割り込み要求をルーティングする場合、システムは、操作で停止可能性があります。 これを防ぐ、カード、カードの INF ファイルで PcmciaExclusiveIrq ディレクティブを配置することで、共有可能な割り込みがサポートされていないことを指定する必要があります。

たとえば、ドライバーには、割り込みの共有をサポートするようになっていない割り込みサービス ルーチン (ISR) が含まれています。 モデムがあるとします。 モデムの INF ファイルで AddReg セクションに次の行を追加して、モデムに固定 ISA 割り込みを割り当てる、オペレーティング システムに指示することができます。

`HKR,,PcmciaExclusiveIrq,0x00010001,1`

ただし、こと PcmciaExclusiveIrq ディレクティブを配置し、デバイスの INF ファイルで、デバイスは機能しないコント ローラー、または ISA 割り込みへのアクセスがないブリッジに注意してください。

 

 





