---
title: NFC クラス拡張インターフェイス
description: NFC CX インターフェイスは、UMDF クラス拡張モデルに基づいています。
ms.assetid: 400043BE-4C16-40C7-B0EB-BA223F882F21
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66b4a2152320e0111fb113e732d596c3c884640a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837749"
---
# <a name="nfc-class-extension-interface"></a>NFC クラス拡張インターフェイス


NFC CX インターフェイスは、UMDF クラス拡張モデルに基づいています。 Nfc CX インターフェイスを使用すると、nfc クライアントは、NFC CX インターフェイスを実装する Microsoft 提供のクラス拡張にクラス実装をオフロードできます。一方、クライアントドライバーは、トランスポート固有の初期化および i/o 処理を実行できます。また、NFC コントローラーに必要なベンダー固有の機能をすべてホストとして使用することもできます。

NFC CX インターフェイスには、次のメソッドが含まれています。

-   [**NfcCxDeviceInitConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitconfig)
-   [**NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)
-   [**NfcCxDeviceDeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdevicedeinitialize)
-   [**Nfccxハードウェアイベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxhardwareevent)
-   [**NfcCxNciReadNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)
-   [**NfcCxSetRfDiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)
-   [**NfcCxSetLlcpConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetllcpconfig)
-   [**NfcCxRegisterSequenceHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxregistersequencehandler)
-   [**NfcCxUnRegisterSequenceHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxunregistersequencehandler)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

