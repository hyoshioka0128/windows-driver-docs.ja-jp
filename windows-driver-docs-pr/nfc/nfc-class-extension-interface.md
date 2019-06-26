---
title: NFC クラスの拡張機能インターフェイス
description: NFC CX のインターフェイスは、UMDF クラスの拡張機能モデルに基づきます。
ms.assetid: 400043BE-4C16-40C7-B0EB-BA223F882F21
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97505807c9c150966db6f4e1d4b4db63566404a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383573"
---
# <a name="nfc-class-extension-interface"></a>NFC クラスの拡張機能インターフェイス


NFC CX のインターフェイスは、UMDF クラスの拡張機能モデルに基づきます。 NFC CX のインターフェイスにより、NFC クライアントは、クラスの実装をクライアント ドライバーとしてトランスポート固有の初期化と、I/O 処理を実行しながら、NFC CX のインターフェイスを実装する Microsoft 提供のクラスの拡張機能をオフロードするにはおよび NFC コント ローラーに必要なすべてのベンダー固有の機能のホストとして機能します。

NFC CX のインターフェイスには、次のメソッドが含まれています。

-   [**NfcCxDeviceInitConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdeviceinitconfig)
-   [**NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdeviceinitialize)
-   [**NfcCxDeviceDeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdevicedeinitialize)
-   [**NfcCxHardwareEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxhardwareevent)
-   [**NfcCxNciReadNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxncireadnotification)
-   [**NfcCxSetRfDiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)
-   [**NfcCxSetLlcpConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxsetllcpconfig)
-   [**NfcCxRegisterSequenceHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxregistersequencehandler)
-   [**NfcCxUnRegisterSequenceHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxunregistersequencehandler)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

