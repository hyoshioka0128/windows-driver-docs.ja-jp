---
title: デバイスとドライバーのインストールの概要
description: デバイスとドライバーのインストールの概要
ms.assetid: 5f29635b-c41b-40d1-8b83-b7f5bc71413b
keywords:
- デバイスのセットアップ WDK デバイスのインストール、デバイスのインストールについて
- デバイスのインストール WDK、デバイスのインストールについて
- デバイスのインストールに関する WDK、デバイスのインストールについて
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: cd853d1644253043b01273b5533523785bec5d72
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007591"
---
# <a name="overview-of-device-and-driver-installation"></a>デバイスとドライバーのインストールの概要





Windows には、デバイスとドライバーをインストールするためのコンポーネントが用意されています。 [システム提供のデバイスインストールコンポーネント](system-provided-device-installation-components.md)は、[ベンダーが提供するコンポーネント](vendor-provided-device-installation-components.md)と連携して、デバイスをインストールします。

Windows は、システムが再起動したとき、およびユーザーがプラグアンドプレイ (PnP) デバイスに接続したとき (または手動で非 PnP デバイスをインストールしたとき) に、デバイスをインストールします。 PnP のサポートでは、ドライバーのインストールを構成するのではなく、システム内のデバイスに基づくデバイスのインストールが続行されます。 たとえば、ドライバーのセットを読み込み、それらのドライバーがサポートしているデバイスを検出するのではなく、Windows はシステム内に存在するデバイスを特定し、各デバイスのドライバーを読み込んで呼び出します。 ACPI ドライバーやその他の PnP[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)などのドライバーは、Windows がどのデバイスを使用しているかを判断するのに役立ちます。

## <a name="in-this-section"></a>このセクションの内容


-   [Windows がデバイスをインストールする方法](how-windows-installs-devices.md)
-   [システムによって提供されるデバイスのインストールコンポーネント](system-provided-device-installation-components.md)
-   [ベンダーが提供するデバイスインストールコンポーネント](vendor-provided-device-installation-components.md)
-   [デバイスのインストールファイル](device-installation-files.md)
-   [デバイスのインストールの種類](device-installation-types.md)
-   [Windows がドライバーを選択する方法](how-setup-selects-drivers.md)

デバイスの管理とインストールの詳細については、[ドライバーのインストール](https://go.microsoft.com/fwlink/p/?linkid=70230)に関する web サイトを参照してください。

 

 





