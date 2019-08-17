---
title: WDM インターフェイスを使用したミニポートドライバーの概要
description: WDM インターフェイスを使用したミニポートドライバーの概要
ms.assetid: defa955b-c1d2-4c78-a983-584aedc8a1a3
keywords:
- ミニポートドライバー WDK ネットワーク、WDM 下位インターフェイス
- NDIS ミニポートドライバー WDK、WDM 下位インターフェイス
- NDIS-WDM ミニポートドライバーの WDK ネットワーク
- WDM 下位インターフェイス WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5955984828ef998a0354e0b318cc770a5af6235e
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565144"
---
# <a name="overview-of-miniport-drivers-with-a-wdm-lower-interface"></a>WDM インターフェイスを使用したミニポートドライバーの概要





Microsoft [Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) (WDM) の下位インターフェイスを備えたミニポートドライバーは、 *NDIS WDM ミニポートドライバー*とも呼ばれます。 この種類のミニポートドライバー:

-   WDM の下端を使用します。

-   は、NDIS と非 NDIS の両方の関数を呼び出すことができます。 ただし、可能な限り、ミニポートドライバーは NDIS 関数を呼び出す必要があります。

-   特定のバスに接続され、そのバスを介してそれらのデバイスと通信するデバイスを制御するために使用されるミニポートインスタンスを初期化できます。

たとえば、Universal Serial Bus (USB) または IEEE 1394 (Firewire) バス上のデバイスを制御するミニポートドライバーでは、標準の NDIS ミニポートドライバーインターフェイスを上端に公開し、その下側の特定のバスに対してクラスインターフェイスを使用する必要があります。 このようなミニポートドライバーは、バスに i/o 要求パケット (Irp) を送信することによってバスに接続されているデバイスと通信します。

次のトピックでは、WDM の下端を使用するミニポートドライバーを実装する方法について説明します。

[WDM 下部のミニポートドライバー](miniport-driver-with-a-wdm-lower-edge.md)

[WDM の下部にミニポートドライバーの機能を登録する](registering-miniport-driver-functions-for-wdm-lower-edge.md)

[WDM 下部のミニポートドライバーの初期化](initializing-a-miniport-driver-with-a-wdm-lower-edge.md)

[デバイスと通信するためのコマンドの発行](issuing-commands-to-communicate-with-devices.md)

[WDM の下部の実装に関するヒントと要件](implementation-tips-and-requirements-for-wdm-lower-edge.md)

[WDM の低速なコンパイルフラグ](compile-flags-for-wdm-lower-edge.md)

[WDM の電源管理の下端](power-management-for-wdm-lower-edge.md)

[NDIS-WDM ミニポートドライバーをインストールしています](installing-ndis-wdm-miniport-drivers.md)

 

 





