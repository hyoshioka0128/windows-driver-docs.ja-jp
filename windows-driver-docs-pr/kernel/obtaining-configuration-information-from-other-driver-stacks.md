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
ms.openlocfilehash: 17813963f5f5435cae131e7848ebca8e500a021d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382905"
---
# <a name="obtaining-configuration-information-from-other-driver-stacks"></a>その他のドライバー スタックからの構成情報の取得





時以外に、ドライバーがある 1 つのスタック上のドライバーがデバイスの構成領域から情報を取得する必要があります。 たとえば、PCI、PCI へのブリッジの構成領域でビットを設定して、ブリッジの PDO へのポインターがありません。 オペレーティング システムでは、PCI、PCI へのブリッジを列挙し、システム上のすべてのブリッジの PDO を作成がこれらのデバイスのデバイスのインターフェイスは登録されません。 そのため、これらのブリッジの構成領域にアクセスするのにデバイス インターフェイス メカニズムを使用することはできません。 デバイス インターフェイスの詳細については、次を参照してください。[デバイス インターフェイスの概要](https://msdn.microsoft.com/library/windows/hardware/ff549460)します。

Windows NT 4.0 では、ドライバーがアクセスを使用してこのようなデバイスの構成領域、 [ **HalGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff546599)と[ **HalSetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff546628)ルーチン。 Windows 2000 および以降のバージョンの Windows では、これは、不要になった場合。

Windows 2000 と Windows の以降のバージョンでは、その他のドライバー スタックに属しているハードウェアにアクセスするドライバーは許可されません。 必要な機能を提供するフィルター ドライバーを記述できます。 たとえば、ブリッジのハードウェアにアクセスする場合は、ブリッジの構成領域で必要な操作を実装するフィルター ドライバーを設計する必要があります。 PnP マネージャーは、ブリッジのデバイス ID を検出した場合に、ブリッジのドライバー スタックに、フィルター ドライバーを読み込むことができますので、ブリッジのハードウェアのハードウェア Id を指定する INF ファイルを指定することも必要があります。

プログラムで使用してフィルターをインストールする代わりに、 **SetupDi * Xxx***、デバイスの共同インストーラー内の関数。

フィルター ドライバーにブリッジを使用して、アクセスできる、 [ **BUS\_インターフェイス\_標準**](https://msdn.microsoft.com/library/windows/hardware/ff540707)インターフェイス。

 

 




