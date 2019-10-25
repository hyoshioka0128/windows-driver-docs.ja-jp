---
title: ISR コンテキスト情報の提供
description: ISR コンテキスト情報の提供
ms.assetid: 216c3111-3638-4410-a720-ff3d65a1eadd
keywords:
- 割り込みサービスルーチン WDK カーネル、コンテキスト情報
- Isr WDK カーネル、コンテキスト情報
- 割り込みオブジェクト WDK カーネル、コンテキスト情報
- コンテキスト情報 WDK 割り込み
- ポインター WDK 割り込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f89f5e97ef52054594f0025e2bf488668b6645e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827580"
---
# <a name="providing-isr-context-information"></a>ISR コンテキスト情報の提供





エントリでは、ISR は、 [**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)を呼び出してルーチンを登録するときに、ドライバーがセットアップした任意のコンテキスト領域へのポインターを受け取ります。

ほとんどのドライバーでは、割り込みを生成する物理デバイスを表すデバイスオブジェクト、またはそのデバイスオブジェクトのデバイス拡張機能にコンテキストポインターを設定します。 デバイス拡張機能では、ドライバーの ISR と[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンの状態情報を格納できます。後者の場合、通常は、デバイスが中断する原因となった各要求を処理するために、ほとんどすべての i/o 処理が実行されます。

通常、ドライバーはデバイス拡張機能を使用して、デバイスの各割り込みオブジェクトへのポインターを格納します ( **IoConnectInterruptEx**への呼び出しから返されます)。 また、通常、ドライバーはデバイス拡張機能に情報を格納します。これにより、isr は、ISR がサポートするデバイスによって割り込みが発行されたかどうかを判断できます。

(または、割り込みオブジェクトポインターは、ドライバーによって割り当てられる非ページプールに格納できます)。

 

 




