---
title: UMDF での USB I/O ターゲット
description: UMDF での USB I/O ターゲット
ms.assetid: e08ca910-1b28-4809-9a5b-db3730cda31a
keywords:
- ユーザー モード ドライバー WDK UMDF、USB I/O ターゲット
- UMDF WDK、USB I/O ターゲット
- ユーザー モード ドライバー フレームワーク WDK、USB I/O ターゲット
- フレームワーク ベースのドライバー WDK UMDF、USB I/O ターゲット
- USB I/O ターゲット WDK UMDF
- USB I/O ターゲット WDK UMDF、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b91ec4da152a3bed45e272c96e6d4e26eae36f7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325948"
---
# <a name="usb-io-targets-in-umdf"></a>UMDF での USB I/O ターゲット

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

各ユニバーサル シリアル バス (USB) デバイスと USB デバイスのインターフェイスをサポートする各パイプは、別の I/O ターゲットを持ちます。 USB デバイスを処理する I/O は、デバイスの I/O のターゲットに送信されます。 特定のパイプ処理する I/O は、そのパイプの I/O のターゲットに送信されます。

## <a name="in-this-section"></a>このセクションの内容


-   [USB デバイスのドライバー モデルの選択](choosing-a-driver-model-for-a-usb-device.md)
-   [特定の USB UMDF 1.x インターフェイス](usb-specific-umdf-1-x-interfaces.md)
-   [UMDF 1.x ドライバーで USB デバイスの操作](working-with-usb-devices-in-umdf-1-x-drivers.md)
-   [UMDF 1.x ドライバーで USB インターフェイスの操作](working-with-usb-interfaces-in-umdf-1-x-drivers.md)
-   [UMDF 1.x ドライバーで USB パイプの使用](working-with-usb-pipes-in-umdf-1-x-drivers.md)
-   [USB I/O ターゲットによってファイルの作成](file-creation-by-a-usb-i-o-target.md)
-   [UMDF から WinUSB の呼び出し](escaping-to-winusb.md)

 

 





