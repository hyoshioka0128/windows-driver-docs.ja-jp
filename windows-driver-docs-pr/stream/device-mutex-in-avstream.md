---
title: AVStream のデバイス ミューテックス
description: AVStream のデバイス ミューテックス
ms.assetid: cec2a040-59d6-44ef-aef1-04f434811d60
keywords:
- AVStream mutexes WDK
- ミュー テックス WDK AVStream
- デバイスのミュー テックス WDK AVStream
- WDK AVStream の同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d31d1ffcbd610162cf3f3084eaf6362aa15884d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360171"
---
# <a name="device-mutex-in-avstream"></a>AVStream のデバイス ミューテックス





フィルターまで、デバイスから階層内のオブジェクトを同期するのにには、デバイスのミュー テックスを使用します。 各 AVStream デバイスでは、1 つの関連付けられているデバイスのミュー テックスを持っています。 両方の作成と破棄は、ファクトリをフィルター処理して、フィルターは、このミュー テックスと同期されます。 特定のプラグ アンド プレイと電源管理操作は、このミュー テックスとも同期されます。 ミニドライバーは、デバイスのミュー テックスに関して 2 つの主な問題について説明します。

オブジェクト階層の安定したことが保証されて*のみ*デバイス ミュー テックスが保持されている場合、個別のフィルターまで、デバイスから。 結果として、ミニドライバーは、手動で呼び出すことによってフィルター ファクトリを作成する前のデバイスのミュー テックスを取得する必要があります[ **KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatefilterfactory)します。 ミニドライバーを呼び出して、オブジェクト階層を移動する前に、デバイスのミュー テックスを取得する必要がありますも、**Ks***Xxx***GetFirstChild * * * Xxx*と **Ks***Xxx***GetNextSibling * * * Xxx*関数。

AVStream は、次の要求を受信すると、ミニドライバーに代わってデバイス ミュー テックスを保持します。

-   [**IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)

-   [**IRP\_MN\_クエリ\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

-   [*PostStart ディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdevice)

-   [**IRP\_MN\_START\_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

-   [**IRP\_MN\_クエリ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

-   [**IRP\_MN\_SET\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

-   スリープし、復帰のフィルターと pin で通知します。 参照してください[ **KsFilterRegisterPowerCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilterregisterpowercallbacks)と[ **KsPinRegisterPowerCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinregisterpowercallbacks)します。

再帰的にことはできませんデバイス ミュー テックスを取得することに注意してください。 次の例を検討してください。 AVStream は、スリープという通知を受け取ります。 前述のよう、ミニドライバーに代わって、デバイスのミュー テックスがかかります。 AVStream し、スレッド A のコンテキストで、ミニドライバーで提供されるコールバック ルーチンを呼び出すと場合、ミニドライバー後しようとしないでスレッド自体でデッドロックが発生するスレッド A A. の実行とデバイスのミュー テックスを取得します。

デバイスのミュー テックスが既に保持されている間、AVStream は多くの場合、フィルター コントロール ミュー テックスを取得します。 その結果、一般的な規則として、スレッド フィルター コントロール ミュー テックスが実行した後で受け取ることはできませんデバイス ミュー テックス。

デバイスのミュー テックスを操作するには、次の関数を使用します。

[**KsAcquireDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksacquiredevice)、 [ **KsReleaseDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksreleasedevice)

 

 




