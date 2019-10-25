---
title: MPIO\_GET\_DESCRIPTOR WMI クラス
description: MPIO\_GET\_DESCRIPTOR WMI クラス
ms.assetid: 6d48c0b5-c20f-4017-aae5-0b00fa5de18d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 57187ac72d935a495df0bb3f2d60e074e740eccc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844968"
---
# <a name="mpio_get_descriptor-wmi-class"></a>MPIO\_GET\_DESCRIPTOR WMI クラス


WMI クライアントは、mpio\_GET\_DESCRIPTOR WMI クラスを使用して、mpio ディスクのデバイスとパスのペアリングを MPIO に照会します。

```cpp
class MPIO_GET_DESCRIPTOR
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Number of instances of this device via different paths.
    //
    [WmiDataId(1),
     read,
     Description("Number of Port Objects backing the device.") : amended
    ] uint32 NumberPdos;

    //
    // Device Name (i.e. MPIODiskN)
    //
    [WmiDataId(2),
     read,
     MaxLen(63),
     Description("Name of Device.") : amended
    ] string DeviceName;

    //
    // Array of device-path pair that form the instances of this device.
    //
    [WmiDataId(3),
     read,
     Description("Array of Information classes describing the real device.") : amended,
     WmiSizeIs("NumberPdos")
    ] PDO_INFORMATION PdoInformation[];
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_GET\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_get_descriptor)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





