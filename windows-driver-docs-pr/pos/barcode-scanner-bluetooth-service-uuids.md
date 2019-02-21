---
title: バーコード スキャナー Bluetooth サービス Uuid
description: このトピックでは、Bluetooth サービス探索プロトコル (SDP) とを使用してバーコード スキャナの Uuid をについて説明します。
ms.assetid: 354654EC-95C8-4BE9-83D3-0926A1E71221
ms.date: 02/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b6a272f76e803de67fe2d7cd3567e7e07fbddee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528688"
---
# <a name="barcode-scanner-bluetooth-service-uuids"></a>バーコード スキャナー Bluetooth サービス Uuid

このトピックでは、Bluetooth サービス探索プロトコル (SDP) とを使用してバーコード スキャナの Uuid をについて説明します。

## <a name="bluetooth-barcode-scanner-uuids"></a>Bluetooth のバーコード スキャナーの Uuid

次の Uuid を使用して、Bluetooth のバーコード スキャナーの検出中に提供するサービスを識別します。

### <a name="ssi-service-uuid"></a>SSI サービス UUID

次の UUID では、Bluetooth のバーコード スキャナーの SSI サービスを識別します。 Bluetooth の検出中にこの UUID を公開しているデバイスは、インボックス ドライバーをサポートするバーコード スキャナーとして認識されます。

```cpp
DEFINE_GUID(BarcodeScannerSimpleSerialInterfaceServiceClass_UUID, 
0xA1220169, 0xE854, 0x473E, 0x9C, 0xB5, 0x87, 0x3A, 0xCB, 0xDF, 0x1F, 0x13)
```

### <a name="reserved-for-future-use"></a>将来使用するために予約されています

次の UUID では、Windows 10 バージョン 1703 ではサポートされていませんが、ISCP で将来使用するために予約されています。

```cpp
DEFINE_GUID(BarcodeScannerIntermecScannerCommunicationProtocolServiceClass_UUID, 
0xccb06baf, 0xdca9, 0x483f, 0x84, 0xd9, 0x36, 0x23, 0x24, 0xce, 0xd, 0x97)
```





