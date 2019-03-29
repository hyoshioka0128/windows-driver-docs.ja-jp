---
title: デバイスとドライバーのインストールの概要
description: デバイスとドライバーのインストールの概要
ms.assetid: 5f29635b-c41b-40d1-8b83-b7f5bc71413b
keywords:
- デバイス セットアップ WDK デバイスのインストール、デバイスのインストールについて
- デバイスのインストールに関するデバイス インストール WDK、
- デバイスのインストールに関するデバイス、WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e5da2f5be09b5193c07a6f01a5b89689a165be8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580679"
---
# <a name="overview-of-device-and-driver-installation"></a>デバイスとドライバーのインストールの概要





Windows では、デバイスとドライバーをインストールするコンポーネントを提供します。 [システム指定のデバイスのインストール コンポーネント](system-provided-device-installation-components.md)と連携して[コンポーネントのベンダーから提供された](vendor-provided-device-installation-components.md)デバイスをインストールします。

Windows デバイスをインストール、システムを再起動すると、システムの再起動後にいつでもユーザーはプラグ アンド プレイ (PnP) デバイスをプラグイン (または非 PnP デバイスを手動でインストールされます)。 サポートに PnP、Windows を実行、ドライバーのインストールを構築するのではなく、システムで、デバイスに基づいているデバイスのインストールします。 一連のドライバーの読み込みではなく、たとえば、あるものとドライバーがサポートされるデバイスを検出、Windows がシステムと負荷に存在するデバイスを決定し、各デバイスのドライバーを呼び出します。 など、ACPI ドライバーおよびその他の PnP ドライバー[バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540704) Windows ヘルプは、デバイスが存在するを決定します。

## <a name="in-this-section"></a>このセクションの内容


-   [Windows がデバイスをインストールする方法](how-windows-installs-devices.md)
-   [システム指定のデバイスのインストール コンポーネント](system-provided-device-installation-components.md)
-   [ベンダー提供のデバイスのインストール コンポーネント](vendor-provided-device-installation-components.md)
-   [デバイスのインストール ファイル](device-installation-files.md)
-   [デバイスのインストールの種類](device-installation-types.md)
-   [Windows ドライバーを選択する方法](how-setup-selects-drivers.md)

デバイスの管理とインストールの詳細については、次を参照してください。、[ドライバーのインストール](https://go.microsoft.com/fwlink/p/?linkid=70230)web サイト。

 

 





