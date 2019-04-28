---
title: PC カードとカード ドライバーの設計のベスト プラクティス
description: PC カードとカード ドライバーの設計のベスト プラクティス
ms.assetid: c3f31757-4063-4c68-ae19-1d8af98f81bc
keywords:
- IRQ ルーティング WDK PCMCIA バス
- PCMCIA WDK バス、IRQ ルーティング
- PC カード WDK PCMCIA バス
- WDK PCMCIA のバスを中断します。
- PCI バスの WDK PCMCIA を中断します。
- ISA は、WDK PCMCIA のバスを中断します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07762164ed7788d85650fa500e75be8e8ae38d5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378282"
---
# <a name="best-practices-for-the-design-of-pc-cards-and-card-drivers"></a>PC カードとカード ドライバーの設計のベスト プラクティス





ベンダーや開発者は、割り込みの共有に関連する問題を回避するために、次の注意事項を確認する必要があります。

-   ドライバー開発者は、共有可能な PCI 割り込みをサポートするドライバーを設計する必要があります。

-   PC カードの製造元は、PCI に準拠しているため、16 ビットの PC カードではなく cardbus を製造する必要があります。

-   すべての 16 ビット PC カードには、共有可能な PCI 割り込みをサポートする必要があります。

-   すべての 16 ビット PC カードは、それらに接続するデバイスの I/O リソースの柔軟な割り当てをサポートする必要があります。 具体的には、カードは I/O 領域の特定の範囲を要求する必要があります。 代わりに、必要があり、柔軟にアドレスを割り当てることを許可する I/O の領域の量を要求する必要があります。

-   コンピューターの製造元は、ISA の Irq を必要とするデバイスがあることに注意する必要があるや、ISA の Irq が CardBus コント ローラーを使用可能なシステムのことを確認する必要があります。

-   コンピューターの製造元は、BIOS のコードが PCIC モードに CardBus コント ローラーを設定することを確認してください。

 

 





