---
title: シリアル コントローラー ドライバー設計ガイド
description: シリアル I/O 要求インターフェイスを使用して、シリアル ポートに接続されている周辺デバイスと通信するドライバーまたはアプリケーションを設計できます。
ms.assetid: 66120e14-20dc-4220-b340-c05cbc59dac8
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: e92cc876a4d4f125577338b34d6dfb7e72e10069
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "63380250"
---
# <a name="serial-controller-driver-design-guide"></a>シリアル コントローラー ドライバー設計ガイド


[シリアル I/O 要求インターフェイス](serial-i-o-request-interface.md)を使用して、シリアル ポートに接続されている周辺デバイスと通信するドライバーまたはアプリケーションを設計できます。 シリアル ポートは、シリアル コントローラー (16550 UART または互換性のあるデバイス) 上のハードウェア通信インターフェイスです。 周辺デバイスが完全に接続されているシリアル ポートを制御するために、シリアル フレームワーク拡張機能 (SerCx2) バージョン 2 (バージョン 1 (SerCx) に代わるもの) と連携するカスタムのシリアル コントローラー ドライバーを設計できます。 または、従来の PC のケースにある名前付きのシリアル ポートを制御するために、インボックスの Serial.sys ドライバーと Serenum.sys ドライバーを使用できます。




## <a name="in-this-section"></a>このセクションの内容


-   [シリアル コントローラー ドライバーの概要](serial-drivers-overview.md)
-   [シリアル フレームワーク拡張機能 (SerCx2) バージョン 2 の使用](using-version-2-of-the-serial-framework-extension.md)
-   [Serial.sys および Serenum.sys の使用](using-serial-sys-and-serenum-sys.md)

 

 




