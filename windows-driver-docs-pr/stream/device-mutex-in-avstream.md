---
title: AVStream のデバイス ミューテックス
description: AVStream のデバイス ミューテックス
ms.assetid: cec2a040-59d6-44ef-aef1-04f434811d60
keywords:
- AVStream ミューテックス WDK
- mutex WDK AVStream
- デバイスミューテックス WDK AVStream
- 同期 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1413f52aef699028839a4ad4c883e892d850431b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826211"
---
# <a name="device-mutex-in-avstream"></a>AVStream のデバイス ミューテックス





デバイスミューテックスを使用して、階層内のオブジェクトをデバイスからフィルターに同期します。 各 AVStream デバイスには、関連付けられた1つのデバイスミューテックスがあります。 フィルターファクトリとフィルターの両方の作成と破棄が、この mutex と同期されます。 特定のプラグアンドプレイおよび電源管理操作も、この mutex と同期されます。 ミニドライバーは、デバイスミューテックスに関して主に2つの問題に焦点を当てています。

オブジェクトの階層は、デバイスのミューテックスが保持されている場合に、デバイスから個別のフィルターまで *、安定し*た状態であることが保証されます。 そのため、ミニドライバーは、 [**KsCreateFilterFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory)を呼び出してフィルターファクトリを手動で作成する前に、デバイスのミューテックスを取得する必要があります。 また、ミニドライバーは、**Ks***xxx***getfirstchild * * * xxx*関数および **ks***xxx***GetNextSibling * * * xxx*関数を呼び出すことによって、オブジェクト階層を走査する前にデバイスのミューテックスを取得する必要があります。

AVStream は、次の要求を受け取ったときに、ミニドライバーに代わってデバイスミューテックスを保持します。

-   [**IRP\_\_クエリ\_\_デバイスの停止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)

-   [**IRP\_\_クエリ\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

-   [*PostStart ディスパッチ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevice)

-   [ **\_デバイスを起動\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)

-   [**IRP\_\_クエリ\_電力**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

-   [**IRP\_\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

-   フィルターとピンのスリープおよびウェイク通知。 「 [**Ksk Filterregisterpowerコールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterregisterpowercallbacks)と[**KsPinRegisterPowerCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinregisterpowercallbacks)」を参照してください。

デバイスミューテックスを再帰的に取得することはできないことに注意してください。 次の例について考えてみましょう。 AVStream はスリープ通知を受け取ります。 前述のように、ミニドライバーの代わりにデバイスのミューテックスを取得します。 AVStream がスレッド A のコンテキストでミニドライバーから提供されるコールバックルーチンを呼び出す場合、ミニドライバーは、その後スレッド a のデバイスミューテックスを取得しようとする必要がありません。これにより、スレッド A がそれ自体でデッドロックする原因になります。

多くの場合、AVStream は、デバイスミューテックスが既に保持されている間、フィルターコントロールのミューテックスを取得します。 そのため、一般的な規則として、フィルターコントロールのミューテックスを取得したスレッドは、その後、デバイスのミューテックスを取得しないようにする必要があります。

デバイスミューテックスを操作するには、次の関数を使用します。

[**KsAcquireDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice)、 [ **ksreleasedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice)

 

 




