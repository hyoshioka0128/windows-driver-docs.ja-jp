---
title: UMDF での USB I/O ターゲット
description: UMDF での USB I/O ターゲット
ms.assetid: e08ca910-1b28-4809-9a5b-db3730cda31a
keywords:
- ユーザーモードドライバー WDK UMDF、USB i/o ターゲット
- UMDF WDK、USB i/o ターゲット
- ユーザーモードドライバーフレームワーク WDK、USB i/o ターゲット
- フレームワークベースのドライバー WDK UMDF、USB i/o ターゲット
- USB i/o ターゲット (WDK UMDF)
- I/o ターゲット WDK UMDF、USB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc4340371a0c9d68227d9ea9c3e731812c593f8
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210774"
---
# <a name="usb-io-targets-in-umdf"></a>UMDF での USB I/O ターゲット

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

各 universal serial bus (USB) デバイスと、USB デバイスインターフェイスがサポートする各パイプには、個別の i/o ターゲットがあります。 USB デバイスが処理する i/o は、デバイスの i/o ターゲットに送信されます。 特定のパイププロセスがそのパイプの i/o ターゲットに送信される i/o。

## <a name="in-this-section"></a>このセクションの内容


-   [USB デバイスのドライバーモデルの選択](choosing-a-driver-model-for-a-usb-device.md)
-   [USB 固有の UMDF 1.x インターフェイス](usb-specific-umdf-1-x-interfaces.md)
-   [UMDF 1.x ドライバーでの USB デバイスの操作](working-with-usb-devices-in-umdf-1-x-drivers.md)
-   [UMDF 1.x ドライバーでの USB インターフェイスの使用](working-with-usb-interfaces-in-umdf-1-x-drivers.md)
-   [UMDF 1.x ドライバーでの USB パイプの使用](working-with-usb-pipes-in-umdf-1-x-drivers.md)
-   [USB i/o ターゲットによるファイルの作成](file-creation-by-a-usb-i-o-target.md)
-   [UMDF から WinUSB を呼び出しています](escaping-to-winusb.md)

 

 





