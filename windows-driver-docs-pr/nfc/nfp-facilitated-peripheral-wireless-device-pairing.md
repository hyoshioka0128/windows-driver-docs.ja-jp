---
title: NFP によるワイヤレス周辺デバイスのペアリング
description: NFP によるワイヤレス周辺デバイスのペアリング
ms.assetid: 7B57019F-C80A-4E74-BBC2-A26BEDEB20DD
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88935187221e5e387936a63f7dd6cc4b31e75fb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378640"
---
# <a name="nfp-facilitated-peripheral-wireless-device-pairing"></a>NFP によるワイヤレス周辺デバイスのペアリング


NFP テクノロジを有効にすることができます、シナリオの 1 つは、Bluetooth キーボード、マウス、ヘッドホンなどのワイヤレス デバイスの Windows でのペアです。 一方向のペアのみがサポートされています。 携帯電話などのスマート デバイスに必要な双方向のペアリングすることはサポートされていません。

この種類のペアリングを実現するために、デバイスは、そのトランスポートに固有のペアリング情報 NFP テクノロジを使用できるようにする必要があります。 場合は、Bluetooth のマウス操作で、マウスが Bluetooth SIG によって定義されている組み合わせについては、標準的な Bluetooth の帯域外 (OOB) を発行する必要があります。 NFP プロバイダーは、デバイスからその OOB データを読み取るし、メッセージの種類のペアリングにサブスクライブしている Windows サービスをする必要があります。

NFP プロバイダーは、理解し、Bluetooth タイプのメッセージのペアを処理する必要があります。 これらは、種類のコンポーネントで識別、 *messageType*パラメーター。 例には、ペアリング: Bluetooth"は静的な Bluetooth OOB がペアリングをサポートするデバイスに対応している可能性があります。 NFP プロバイダーは、メッセージをペアリングする次のいずれかを受信すると、標準 OOB (NDEF ヘッダー) のようなテクノロジに固有のプロトコル情報を削除するデータのペアを単にメッセージを変換にする必要があります。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

