---
title: SD カードの割り込みの処理
description: SD カードの割り込みの処理
ms.assetid: 40c18af4-6b23-4893-b82f-7fe652929069
keywords:
- SD WDK バス、割り込み
- WDK SD バスを中断します。
- Irql WDK SD バス
- ハードウェアの割り込みの WDK SD バス
- 割り込み通知 WDK SD バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d467715aeced4d5f3f34643d50b04c48457cc16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384515"
---
# <a name="handling-sd-card-interrupts"></a>SD カードの割り込みの処理


セキュリティで保護されたデジタル (SD) カードのドライバーには割り込みサービス ルーチン (Isr) がないと、割り込み要求 (IRQ) のリソースを取得しません。 SD バス ドライバー検出しハードウェアの割り込みをインターセプトし、割り込み通知コールバック ルーチンを使用して、デバイス ドライバーを報告[ **PSDBUS\_コールバック\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nc-ntddsd-sdbus_callback_routine)セクションで説明したように[セキュア デジタル (SD) ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/sd/sd-card-driver-stack)と[を開くと、SD バスのインターフェイスの初期化](https://docs.microsoft.com/windows-hardware/drivers/sd/opening--initializing-and-closing-an-sd-card-bus-interface)します。

デバイス ドライバーを割り込み、割り込み通知コールバック ルーチンのコンテキストで処理を完了する必要はありません。 ドライバーでは、コールバック ルーチンから返すでき、独自のコンテキストでの割り込み処理を完了することができます。 ドライバーでは、割り込みの処理が完了したら、SD バスのインターフェイスで提供される割り込みの受信確認ルーチンを明示的に呼び出す、バス ドライバーに通知します。 割り込みの受信確認のルーチンの詳細については、次を参照してください。 [ **PSDBUS\_ACKNOWLEDGE\_INT\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nc-ntddsd-psdbus_acknowledge_int_routine)します。 バス ドライバーでは、この呼び出しを受信すると、割り込み再できます。

SD デバイス ドライバーでは、実行順序に IRQ レベル (Irql) に関して 2 つのオプションがあります。 パッシブ排他的に実行できる、SD ドライバー\_レベル、またはそれがディスパッチでも実行できます\_パッシブに、割り込み通知コールバック ルーチンのコンテキストの中にレベル\_レベル、残りの時間。 SD のデバイス ドライバーをパッシブ排他的に実行すると\_レベル、バス ドライバーは、割り込みを同期するための責任を負います。 ドライバーのデザインが簡単になりますので、割り込みの待機時間に厳密な制限のないデバイスを運用ことができる場合は、このオプションを選択します。 バス ドライバーに割り込み同期のタスクをオフロードするには、その他の特典があります。 たとえば、ドライバーは、割り込みに応答してデータを頻繁に転送する必要があります。 パッシブに、ドライバーのコールバック ルーチンが実行されている場合\_レベルが自由に非同期ではなく、同期 I/O 操作を実行します。 ディスパッチにコールバック ルーチンが実行する場合\_レベル、下位の IRQL で同期 I/O を実行する前に実行されるまで、ドライバーを待つ必要があります。

SD のデバイス ドライバーには、実行する SD バスのインターフェイスを初期化するときは IRQL を指定します。 ディスパッチで実行する\_レベル、割り込み通知コールバック ルーチンで、ドライバーを設定する必要があります、 **CallbackAtDpcLevel**のメンバー、 [ **SDBUS\_インターフェイス\_パラメーター** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))構造体を**TRUE**インターフェイスの初期化ルーチンをこの構造体を渡します。 インターフェイスのルーチンの説明は、次を参照してください。 [ **PSDBUS\_初期化\_インターフェイス\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)します。 パッシブでのみ実行する\_レベル、ドライバーを設定する必要があります**CallbackAtDpcLevel**に**FALSE**します。

 

 




