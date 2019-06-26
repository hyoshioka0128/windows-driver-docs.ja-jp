---
title: WDM の下位インターフェイスを含むミニポート ドライバー
description: WDM の下位インターフェイスを含むミニポート ドライバー
ms.assetid: defa955b-c1d2-4c78-a983-584aedc8a1a3
keywords:
- ミニポート ドライバー WDK ネットワー キング、WDM 低いインターフェイス
- NDIS ミニポート ドライバー WDK、WDM 削減インターフェイス
- NDIS WDM ミニポート ドライバー WDK ネットワーク
- WDM 低いインターフェイス WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e75d2d1d3e5e028458dd7508a63518788e8f070a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380890"
---
# <a name="miniport-drivers-with-a-wdm-lower-interface"></a>WDM の下位インターフェイスを含むミニポート ドライバー





Microsoft のミニポート ドライバー [Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) (WDM) 下位インターフェイスとも呼ばれますが、 *NDIS WDM ミニポート ドライバー*します。 この種類のミニポート ドライバーでは:

-   WDM 下端を使用します。

-   両方の NDIS および NDIS 以外の関数を呼び出すことができます。 ただし、可能であれば、ミニポート ドライバーは NDIS 関数を呼び出す必要があります。

-   そのバス経由でそれらのデバイスで特定のバスに接続されていると通信する、デバイスを制御するために使用するミニポート インスタンスを初期化できます。

たとえば、ユニバーサル シリアル バス (USB) または IEEE 1394 (Firewire) バス上のデバイスを制御するミニポート ドライバーは、上端にある標準の NDIS ミニポート ドライバー インターフェイスを公開し、クラス インターフェイスの下の端に特定のバスを使用する必要があります。 このようなミニポート ドライバー、バスに I/O 要求パケット (Irp) を送信することによって、バスに接続されているデバイスと通信します。

次のトピックでは、WDM 下端を使用するミニポート ドライバーを実装する方法について説明します。

[WDM 下端のミニポート ドライバー](miniport-driver-with-a-wdm-lower-edge.md)

[WDM 下端のミニポート ドライバー関数を登録します。](registering-miniport-driver-functions-for-wdm-lower-edge.md)

[WDM 下端のミニポート ドライバーの初期化](initializing-a-miniport-driver-with-a-wdm-lower-edge.md)

[デバイスと通信するためのコマンドを発行します。](issuing-commands-to-communicate-with-devices.md)

[実装のヒントと WDM 下端の要件](implementation-tips-and-requirements-for-wdm-lower-edge.md)

[WDM 下端のフラグをコンパイルします。](compile-flags-for-wdm-lower-edge.md)

[WDM 下端の電源管理](power-management-for-wdm-lower-edge.md)

[NDIS WDM ミニポート ドライバーをインストールします。](installing-ndis-wdm-miniport-drivers.md)

 

 





