---
title: 割り込みサービスルーチンの概要
description: 割り込みサービスルーチンの概要
ms.assetid: e83eb873-7cdf-4faf-9a6e-cc5954ebf1d6
keywords:
- 割り込みサービスルーチンの WDK カーネル、Isr について
- Isr WDK カーネル、割り込みサービスルーチンについて
- InterruptService
- 行ベースの割り込み (WDK カーネル)
- 割り込み回線 WDK カーネル
- メッセージシグナル割り込み (WDK カーネル)
- InterruptMessageService
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93e9545b199b9a5186b3bf49a63c10442fa935d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838623"
---
# <a name="introduction-to-interrupt-service-routines"></a>割り込みサービスルーチンの概要


割り込みを受け取る物理デバイスのドライバーは、割り込みを処理するために1つまたは複数の割り込みサービスルーチン (ISR) を登録します。 システムは、その割り込みを受信するたびに ISR を呼び出します。

PCI 2.2 より前のポートおよびバスのデバイスでは、*行ベースの割り込み*が生成されます。 デバイスは、*割り込み線*と呼ばれる専用の pin で電気信号を送信することによって、割り込みを生成します。 Windows Vista より前のバージョンの Microsoft Windows では、行ベースの割り込みのみがサポートされています。

PCI 2.2 以降では、PCI デバイスは*メッセージシグナル割り込み*を生成できます。 デバイスは、特定のアドレスにデータ値を書き込むことによって、メッセージシグナル割り込みを生成します。 Windows Vista 以降のオペレーティングシステムでは、行ベースとメッセージシグナルの両方の割り込みがサポートされています。

システムでは、次の2種類の Isr がサポートされています。

-   ドライバーは、 [*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンを登録して、行ベースまたはメッセージシグナルの割り込みを処理できます。 (これは、Windows Vista より前に使用できる唯一の種類です)。システムは、ドライバーによって提供されるコンテキスト値を渡します。

-   ドライバーは、 [*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)ルーチンを登録して、メッセージシグナル割り込みを処理できます。 システムは、ドライバーによって提供されるコンテキスト値と割り込みメッセージのメッセージ ID の両方を渡します。

InterruptService または InterruptMessageService ルーチンを登録してデバイスの割り込みを処理する方法の詳細については、「[メッセージシグナル割り込みの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-message-signaled-interrupts)」を参照してください。
 

 




