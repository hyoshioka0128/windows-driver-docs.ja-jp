---
title: SD カードの割り込みの処理
description: SD カードの割り込みの処理
ms.assetid: 40c18af4-6b23-4893-b82f-7fe652929069
keywords:
- SD WDK バス、割り込み
- WDK SD bus を中断します
- IRQLs WDK SD bus
- ハードウェア割り込み WDK SD バス
- 割り込み通知 WDK SD bus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 299761d9bd1ed76b8719f98554d8616e6346fdc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844485"
---
# <a name="handling-sd-card-interrupts"></a>SD カードの割り込みの処理


セキュアデジタル (SD) カードドライバーは、割り込みサービスルーチン (Isr) を持たず、割り込み要求 (IRQ) リソースを取得しません。 SD bus ドライバーは、ハードウェアの割り込みを検出して傍受し、「セキュリティで保護されたデジタル (」セクションで説明されているように、割り込み通知コールバックルーチン[**PSDBUS\_コールバック\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-sdbus_callback_routine)を通じてデバイスドライバーに報告します。 [SD) ドライバースタック](https://docs.microsoft.com/windows-hardware/drivers/sd/sd-card-driver-stack)を[開き、Sd バスインターフェイスを開いて初期](https://docs.microsoft.com/windows-hardware/drivers/sd/opening--initializing-and-closing-an-sd-card-bus-interface)化します。

デバイスドライバーは、割り込み通知コールバックルーチンのコンテキストで割り込み処理を完了する必要はありません。 このドライバーは、コールバックルーチンから戻り、独自のコンテキストで割り込み処理を完了することができます。 ドライバーは、割り込みの処理を完了すると、SD bus インターフェイスによって提供される割り込み受信確認ルーチンへの明示的な呼び出しによってバスドライバーに通知します。 割り込み受信確認ルーチンの詳細については、「 [**PSDBUS\_\_INT\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_acknowledge_int_routine)」を参照してください。 バスドライバーは、この呼び出しを受信すると、割り込みを再び有効にします。

SD デバイスドライバーには、実行する IRQ レベル (IRQLs) に関して2つのオプションがあります。 SD ドライバーは、パッシブ\_レベルでのみ実行できます。または、割り込み通知のコールバックルーチンのコンテキスト内、および残りの時間のパッシブ\_レベルで、ディスパッチ\_レベルで実行できます。 SD デバイスドライバーがパッシブ\_レベルで排他的に実行される場合、バスドライバーは割り込みの同期を担います。 ドライバーの設計を簡素化するため、デバイスが割り込み待機時間に厳密に制限されずに動作する場合は、このオプションを選択します。 バスドライバーに対する割り込み同期のタスクをオフロードするだけでなく、他にも利点があります。 たとえば、ドライバーは、割り込みに応答してデータを頻繁に転送する必要があります。 ドライバーのコールバックルーチンがパッシブ\_レベルで実行されている場合、非同期の i/o 操作を実行することはできません。 コールバックルーチンがディスパッチ\_レベルで実行される場合、ドライバーは、同期 i/o を行う前に、低い IRQL で実行されるまで待機する必要があります。

SD デバイスドライバーは、SD バスインターフェイスを初期化するときに実行される IRQL を指定します。 割り込み通知のコールバックルーチンでディスパッチ\_レベルで実行するには、ドライバーは[**Sdbus\_\_インターフェイス**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))の**CallbackAtDpcLevel**メンバーを**TRUE**に設定し、この構造体をに渡します。インターフェイス初期化ルーチン。 インターフェイスルーチンの詳細については、「 [**PSDBUS\_INITIALIZE\_interface\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)」を参照してください。 パッシブ\_レベルでのみ実行するには、ドライバーで**CallbackAtDpcLevel**を**FALSE**に設定する必要があります。

 

 




