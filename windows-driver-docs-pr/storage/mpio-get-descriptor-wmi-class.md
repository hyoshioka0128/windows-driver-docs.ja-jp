---
title: MPIO\_取得\_記述子 WMI クラス
description: MPIO\_取得\_記述子 WMI クラス
ms.assetid: 6d48c0b5-c20f-4017-aae5-0b00fa5de18d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bfa511e242532c031319c895e8e807cc9bf94b33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383062"
---
# <a name="mpiogetdescriptor-wmi-class"></a>MPIO\_取得\_記述子 WMI クラス


WMI クライアントが、MPIO を使用して\_取得\_記述子の WMI クラスの MPIO の MPIO ディスクのデバイス パスの組み合わせをクエリします。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_取得\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562398)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





