---
title: その他のドライバー スタックからの構成情報の取得
description: その他のドライバー スタックからの構成情報の取得
ms.assetid: ca0f3d51-24c6-44df-828f-6aeb2565c1ae
keywords:
- I/o WDK カーネル、デバイス構成領域
- デバイス構成領域 WDK i/o
- 構成領域の WDK i/o
- 領域 WDK i/o
- ドライバースタック WDK の構成情報
- BUS_INTERFACE_STANDARD
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55878ba280d2fe1464fc1cd029aa7ae95e0ff72e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827767"
---
# <a name="obtaining-configuration-information-from-other-driver-stacks"></a>その他のドライバー スタックからの構成情報の取得





ドライバーが含まれているもの以外のスタック上にあるデバイスの構成領域から情報を取得する必要がある場合があります。 たとえば、PCI から PCI へのブリッジの構成領域にビットを設定し、ブリッジの PDO へのポインターを持っていないとします。 オペレーティングシステムは、PCI から PCI へのブリッジを列挙し、システム上のすべてのブリッジ用に PDO を作成しますが、これらのデバイスのデバイスインターフェイスは登録しません。 そのため、デバイスインターフェイス機構を使用して、これらのブリッジの構成領域にアクセスすることはできません。 デバイスインターフェイスの詳細については、「[デバイスインターフェイスの概要」を](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)参照してください。

Windows NT 4.0 では、ドライバーは[**HalGetBusData**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))ルーチンと[**HalSetBusData**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))ルーチンを使用して、このようなデバイスの構成領域にアクセスできます。 Windows 2000 以降のバージョンの Windows では、これは不要になりました。

Windows 2000 以降のバージョンの Windows では、ドライバーが他のドライバースタックに属するハードウェアにアクセスすることは許可されていません。 フィルタードライバーは、必要な機能を提供するために記述できます。 たとえば、ブリッジハードウェアにアクセスする場合は、ブリッジの構成領域に対して必要な操作を実装するフィルタードライバーを設計する必要があります。 また、ブリッジハードウェアの可能性のあるハードウェア Id を指定する INF ファイルを指定する必要があります。これにより、PnP マネージャーは、ブリッジのデバイス ID を検出したときに、フィルタードライバーをブリッジのドライバースタックに読み込むことができます。

または、デバイスの共同インストーラーで**Setupdi<em>Xxx</em>** 関数を使用して、プログラムでフィルターをインストールすることもできます。

フィルタードライバーは、[**バス\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)インターフェイスを使用してブリッジにアクセスできます。

 

 




