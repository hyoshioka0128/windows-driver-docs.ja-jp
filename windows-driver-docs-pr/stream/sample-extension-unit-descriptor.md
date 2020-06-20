---
title: サンプル拡張ユニット記述子
description: サンプル拡張ユニット記述子
ms.assetid: 283a28e6-9f73-4131-bcfb-b4983a92cecd
keywords:
- 拡張機能ユニット記述子 WDK USB ビデオクラス
- 記述子 WDK USB ビデオクラス
- 記述子 WDK USB ビデオクラス、サンプルコード
- サンプルコード WDK USB ビデオクラス、拡張機能単位記述子
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: f300d2ea5b06d1af006a7c06cb85e1de41d1e297
ms.sourcegitcommit: f29360d62eb77b6ee875ce66483d5bc72785eede
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85111246"
---
# <a name="sample-extension-unit-descriptor"></a>拡張機能の単位記述子のサンプル

このコードは、ハードウェアレベルで拡張単位記述子を提供する方法を示しています。

```cpp
BYTE  Length:            0x1a
BYTE  DescriptorType:    0x24
BYTE  DescriptorSubtype: 0x06
BYTE  bUnitID:           0x05
GUID  guidExtensionCode: xxxxxxxx-xxxx-xxxx-xxxxxxxxxxxxxxxx
BYTE  bNumControls:      0x03
BYTE  bNrInPins:         0x01
BYTE  baSourceID[0]:     0x01
```

USB ビデオクラスのハードウェア要件の詳細については、*ビデオデバイス仕様のユニバーサルシリアルバスデバイスクラス定義*に関する説明を参照してください。 この仕様は、 [USB 実装者フォーラム](https://www.usb.org/)の web サイトで入手できます。
