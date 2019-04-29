---
title: サンプル拡張ユニット記述子
description: サンプル拡張ユニット記述子
ms.assetid: 283a28e6-9f73-4131-bcfb-b4983a92cecd
keywords:
- 拡張機能ユニット記述子 WDK USB ビデオ クラス
- 記述子 WDK USB ビデオ クラス
- 記述子のサンプル コードの WDK USB ビデオ クラス
- サンプル コード WDK USB ビデオ クラスの拡張単位記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e48e469e0016179d1be1e05f2bc08f4daa7edc0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389212"
---
# <a name="sample-extension-unit-descriptor"></a>サンプル拡張ユニット記述子


このコードでは、ハードウェア レベルで、拡張機能ユニット記述子を提供する方法を示します。

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

USB ビデオ クラスのハードウェア要件について詳細を参照してください、*ユニバーサル シリアル バス デバイスのクラス定義ビデオ DevicesSpecification*します。 この仕様は、 [USB Implementers Forum](https://go.microsoft.com/fwlink/p/?linkid=8780) web サイト。

 

 




