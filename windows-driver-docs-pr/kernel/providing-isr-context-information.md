---
title: ISR コンテキスト情報の提供
description: ISR コンテキスト情報の提供
ms.assetid: 216c3111-3638-4410-a720-ff3d65a1eadd
keywords:
- 割り込みサービス ルーチン WDK カーネル、コンテキスト情報
- Isr WDK カーネルでは、コンテキスト情報
- 割り込みオブジェクト WDK カーネル、コンテキスト情報
- コンテキスト情報 WDK の割り込み
- ポインターの WDK の割り込み
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee25ae21753e0976f1bb1a46c678796ae2d3a79b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378785"
---
# <a name="providing-isr-context-information"></a>ISR コンテキスト情報の提供





エントリの ISR はドライバーを設定することが呼び出されたときにどのようなコンテキスト領域へのポインターを受け取る[ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)ルーチンを登録します。

ほとんどのドライバーは、割り込みを生成する物理デバイスを表すデバイス オブジェクトまたはそのデバイス オブジェクトのデバイスの拡張機能にコンテキスト ポインターを設定します。 デバイス拡張機能では、ドライバーがドライバーの ISR の状態情報を格納できますと[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン、後者のうち、通常はほぼすべてを満たす各 I/O 処理の要求中断するデバイスを発生します。

通常、ドライバーの各デバイスの割り込みのオブジェクトへのポインターを格納するデバイスの拡張機能を使用して、(への呼び出しから返された**IoConnectInterruptEx**)。 ドライバーは、ISR、割り込みが ISR サポートしているデバイスによって発行されたかどうかを判断することができるデバイスの拡張機能にも通常情報を格納します。

(または、割り込みオブジェクト ポインターは、ドライバーによって割り当てられる非ページ プールに格納できます。)

 

 




