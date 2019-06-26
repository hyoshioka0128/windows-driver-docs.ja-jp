---
title: MPIO\_ディスク\_ヘルス\_情報 WMI クラス
description: MPIO\_ディスク\_ヘルス\_情報 WMI クラス
ms.assetid: 5a3ca8be-8940-4ba4-9206-75d0c7c90d53
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26f557913e60f271c03c4dd4ee10a2ee52c05abd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386165"
---
# <a name="mpiodiskhealthinfo-wmi-class"></a>MPIO\_ディスク\_ヘルス\_情報 WMI クラス


MPIO ドライバーは、MPIO を使用して\_ディスク\_ヘルス\_情報 WMI クラスを管理しているすべての MPIO のディスクの正常性の統計情報を報告します。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_ディスク\_正常性\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_disk_health_info)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





