---
title: 割り込みサービス ルーチンの概要
description: 割り込みサービス ルーチンの概要
ms.assetid: e83eb873-7cdf-4faf-9a6e-cc5954ebf1d6
keywords:
- 割り込みサービス ルーチン WDK カーネルでは、Isr について
- 割り込みサービス ルーチンについての Isr WDK カーネル
- InterruptService
- 行ベースの割り込み WDK カーネル
- 割り込み行 WDK カーネル
- メッセージ シグナル割り込み WDK カーネル
- InterruptMessageService
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9abcb3032a9003aa774e3b764f77fbce850b713
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369729"
---
# <a name="introduction-to-interrupt-service-routines"></a>割り込みサービス ルーチンの概要


割り込みを受信する物理デバイスのドライバーでは、1 つまたは複数の割り込みサービス ルーチン (ISR)、割り込みをサービスに登録します。 システムでは、その割り込みを受信するたびに、ISR を呼び出します。

ポートおよび PCI 2.2 より前のバスのデバイス生成*行ベースの割り込み*します。 デバイスと呼ばれる専用の pin の電気の信号を送信することによって、割り込みを生成する、*行を中断*します。 Windows Vista より前に、Microsoft Windows のバージョンでは、行ベースの割り込みのみサポートします。

PCI 2.2 以降では、PCI デバイスが生成できる*メッセージ シグナル割り込み*します。 デバイスは、特定のアドレスにデータ値を記述することで、メッセージ シグナル割り込みを生成します。 Windows Vista およびそれ以降のオペレーティング システムは、行に基づくし、メッセージ シグナル割り込みをサポートします。

システムには、isr を特定の 2 つのさまざまな種類がサポートされています。

-   ドライバーが登録できる、 [ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)行ベースまたはメッセージ シグナル割り込みを処理するルーチン。 (これは、Windows Vista より前に使用可能な唯一の種類です)。システムでは、ドライバーによって提供されるコンテキストの値を渡します。

-   ドライバーが登録できる、 [ *InterruptMessageService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)メッセージ シグナル割り込みを処理するルーチン。 システムでは、ドライバーによって提供されるコンテキストの値と、割り込みメッセージのメッセージ ID の両方を渡します。

InterruptService または InterruptMessageService ルーチンで、デバイスの割り込みをサービスの登録の詳細については、次を参照してください。 [Message-Signaled 割り込み概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-message-signaled-interrupts)します。
 

 




