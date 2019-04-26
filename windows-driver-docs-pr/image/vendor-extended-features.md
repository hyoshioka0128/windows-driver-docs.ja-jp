---
title: ベンダー拡張機能
description: ベンダー拡張機能
ms.assetid: 8063622e-efc4-4940-893f-2916bf297d12
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfd697a934ce8b04fe13b3d117e73b30b23ef7ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356120"
---
# <a name="vendor-extended-features"></a>ベンダー拡張機能





このセクションには、ベンダー拡張機能、PTP がについて説明しますデバイスは、これらの拡張機能を公開する方法と、次をサポートできます。

[PTP のカメラのベンダー拡張機能を公開します。](exposing-the-vendor-extensions-of-your-ptp-camera.md)

[ベンダー拡張プロパティ](vendor-extended-properties.md)

[ベンダー拡張イベント](vendor-extended-events.md)

[ベンダー拡張コマンド](vendor-extended-commands.md)

ベンダー拡張プロパティとイベントに表示する必要があります、 **DeviceData** INF ファイルのエントリと、イベントが内の名前を指定する必要があります、**イベント**INF ファイルのエントリ (を参照してください[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)詳細については)。 ベンダー拡張機能の ID を一覧表示するエントリが必要です。 これに一致する必要があります、 **VendorExtensionID** DeviceInfo データセットのフィールド。 その他のエントリの例が次のとおりし、次のセクションで説明します。

```INF
[DeviceData]
VendorExtID=0x12345678
PropCode="0xD001,0xD002,0xD003"
PropCodeD001="0x00009802,Vendorproperty1"
PropCodeD002="0x00009803,Vendorproperty2"
PropCodeD003="0x00009804,Vendorproperty3"
EventCode="0xC001,0xC002"
EventCodeC001={191D9AE7-EE8C-443c-B3E8-A3F87E0CF3CC}
EventCodeC002={8162F5ED-62B7-42c5-9C2B-B1625AC0DB93}

[Events]
EventCodeC001="Vendorevent1",{191D9AE7-EE8C-443c-B3E8-A3F87E0CF3CC},*
EventCodeC002="Vendorevent2",{8162F5ED-62B7-42c5-9C2B-B1625AC0DB93},*
```

**注**   WIA デバイス用の INF ファイル、仕入先プロパティの名前は、スペースなしで、1 つの単語にする必要があり、英数字の値のみで構成されています。

 

 

 




