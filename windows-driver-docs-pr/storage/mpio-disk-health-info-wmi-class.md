---
title: MPIO\_DISK\_HEALTH\_INFO WMI クラス
description: MPIO\_DISK\_HEALTH\_INFO WMI クラス
ms.assetid: 5a3ca8be-8940-4ba4-9206-75d0c7c90d53
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 884804b867f4800c6357ce76874ab2685266febd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844977"
---
# <a name="mpio_disk_health_info-wmi-class"></a>MPIO\_DISK\_HEALTH\_INFO WMI クラス


Mpio ドライバーは、MPIO\_DISK\_HEALTH\_INFO WMI クラスを使用して、管理対象のすべての MPIO ディスクの正常性の統計情報をレポートします。

```cpp
class MPIO_DISK_HEALTH_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    [WmiDataId(1),
     read,
     Description("Number of Pseudo-LUN Health Packets.") : amended
    ] uint32 NumberDiskPackets;

    [WmiDataId(2),
     read,
     Description("Reserved for future use.") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     Description("MPIO Pseudo-LUN Health Info Array.") : amended,
     WmiSizeIs("NumberDiskPackets")
    ] MPIO_DISK_HEALTH_CLASS DiskHealthPackets[];
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_DISK\_HEALTH\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_disk_health_info)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





