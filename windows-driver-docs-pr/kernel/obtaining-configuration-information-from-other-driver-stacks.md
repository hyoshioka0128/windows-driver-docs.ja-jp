---
title: その他のドライバー スタックからの構成情報の取得
description: その他のドライバー スタックからの構成情報の取得
ms.assetid: ca0f3d51-24c6-44df-828f-6aeb2565c1ae
keywords:
- デバイス構成領域、I/O の WDK カーネル
- デバイス構成領域 WDK I/O
- 構成領域 WDK I/O
- WDK の I/O の領域
- ドライバー スタック WDK 構成情報
- BUS_INTERFACE_STANDARD
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f669fab6b62f25ceeb82143c60d3aa6d54834b86
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716976"
---
# <a name="obtaining-configuration-information-from-other-driver-stacks"></a>その他のドライバー スタックからの構成情報の取得





時以外に、ドライバーがある 1 つのスタック上のドライバーがデバイスの構成領域から情報を取得する必要があります。 たとえば、PCI、PCI へのブリッジの構成領域でビットを設定して、ブリッジの PDO へのポインターがありません。 オペレーティング システムでは、PCI、PCI へのブリッジを列挙し、システム上のすべてのブリッジの PDO を作成がこれらのデバイスのデバイスのインターフェイスは登録されません。 そのため、これらのブリッジの構成領域にアクセスするのにデバイス インターフェイス メカニズムを使用することはできません。 デバイス インターフェイスの詳細については、次を参照してください。[デバイス インターフェイスの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)します。

Windows NT 4.0 では、ドライバーがアクセスを使用してこのようなデバイスの構成領域、 [ **HalGetBusData** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))と[ **HalSetBusData** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))ルーチン。 Windows 2000 および以降のバージョンの Windows では、これは、不要になった場合。

Windows 2000 と Windows の以降のバージョンでは、その他のドライバー スタックに属しているハードウェアにアクセスするドライバーは許可されません。 必要な機能を提供するフィルター ドライバーを記述できます。 たとえば、ブリッジのハードウェアにアクセスする場合は、ブリッジの構成領域で必要な操作を実装するフィルター ドライバーを設計する必要があります。 PnP マネージャーは、ブリッジのデバイス ID を検出した場合に、ブリッジのドライバー スタックに、フィルター ドライバーを読み込むことができますので、ブリッジのハードウェアのハードウェア Id を指定する INF ファイルを指定することも必要があります。

プログラムで使用してフィルターをインストールする代わりに、 **SetupDi<em>Xxx</em>** デバイスの共同インストーラー内の関数。

フィルター ドライバーにブリッジを使用して、アクセスできる、 [ **BUS\_インターフェイス\_標準**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_bus_interface_standard)インターフェイス。

 

 




