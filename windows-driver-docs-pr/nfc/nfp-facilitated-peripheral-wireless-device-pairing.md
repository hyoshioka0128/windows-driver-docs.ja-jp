---
title: NFP-周辺のワイヤレスデバイスのペアリングの促進
description: NFP-周辺のワイヤレスデバイスのペアリングの促進
ms.assetid: 7B57019F-C80A-4E74-BBC2-A26BEDEB20DD
keywords:
- NFC
- 近距離無線通信
- 近く
- 近距離フィールド近接
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70eda4791fc6abc95525372b6ffdcc9a87c419ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838884"
---
# <a name="nfp-facilitated-peripheral-wireless-device-pairing"></a>NFP-周辺のワイヤレスデバイスのペアリングの促進


NFP テクノロジで有効にできるシナリオの1つは、Bluetooth キーボード、マウス、ヘッドホンなどのワイヤレスデバイスの Windows とのペアリングです。 一方向のペアリングのみがサポートされています。 携帯電話などのスマートデバイスで必要とされる双方向ペアリングはサポートされていません。

このようなペアリングを実現するために、デバイスは、NFP テクノロジでトランスポート固有のペアリング情報を使用できるようにする必要があります。 Bluetooth マウスの場合、マウスは、Bluetooth SIG で定義されているように、標準の Bluetooth 帯域外 (OOB) ペアリング情報を発行する必要があります。 NFP プロバイダーは、デバイスからその OOB データを読み取って、型メッセージのペアリングをサブスクライブしている Windows サービスに渡す必要があります。

NFP プロバイダーは、Bluetooth ペアリングの種類のメッセージを理解し、処理する必要があります。 これらは、 *messageType*パラメーターの type コンポーネントによって識別されます。 例としては、Bluetooth OOB の静的ペアリングをサポートするデバイスに対応する "ペアリング: Bluetooth" などがあります。 NFP プロバイダーは、これらのペアリングメッセージのいずれかを受信すると、メッセージを標準の OOB ペアリングデータだけに変換し、テクノロジ固有のプロトコル情報 (NDEF ヘッダーなど) を削除する必要があります。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

