---
title: NFC クラスの拡張機能インターフェイス
description: NFC CX のインターフェイスは、UMDF クラスの拡張機能モデルに基づきます。
ms.assetid: 400043BE-4C16-40C7-B0EB-BA223F882F21
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60d7e74f98e30aa4ff0f22085b1be7ddff40ca5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551940"
---
# <a name="nfc-class-extension-interface"></a>NFC クラスの拡張機能インターフェイス


NFC CX のインターフェイスは、UMDF クラスの拡張機能モデルに基づきます。 NFC CX のインターフェイスにより、NFC クライアントは、クラスの実装をクライアント ドライバーとしてトランスポート固有の初期化と、I/O 処理を実行しながら、NFC CX のインターフェイスを実装する Microsoft 提供のクラスの拡張機能をオフロードするにはおよび NFC コント ローラーに必要なすべてのベンダー固有の機能のホストとして機能します。

NFC CX のインターフェイスには、次のメソッドが含まれています。

-   [**NfcCxDeviceInitConfig**](https://msdn.microsoft.com/library/windows/hardware/dn905610)
-   [**NfcCxDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905611)
-   [**NfcCxDeviceDeinitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905609)
-   [**NfcCxHardwareEvent**](https://msdn.microsoft.com/library/windows/hardware/dn905612)
-   [**NfcCxNciReadNotification**](https://msdn.microsoft.com/library/windows/hardware/dn905613)
-   [**NfcCxSetRfDiscoveryConfig**](https://msdn.microsoft.com/library/windows/hardware/dn905616)
-   [**NfcCxSetLlcpConfig**](https://msdn.microsoft.com/library/windows/hardware/dn905615)
-   [**NfcCxRegisterSequenceHandler**](https://msdn.microsoft.com/library/windows/hardware/dn905614)
-   [**NfcCxUnRegisterSequenceHandler**](https://msdn.microsoft.com/library/windows/hardware/dn905617)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

