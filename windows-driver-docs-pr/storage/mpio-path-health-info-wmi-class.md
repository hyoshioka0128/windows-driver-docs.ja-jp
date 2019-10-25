---
title: MPIO\_パス\_正常性\_情報 WMI クラス
description: MPIO\_パス\_正常性\_情報 WMI クラス
ms.assetid: 26c329d0-0d9c-4d24-bbe4-ebb7d7b36a89
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d2d8939b5c88914de4c8d8da497cabb999f5b267
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844961"
---
# <a name="mpio_path_health_info-wmi-class"></a>MPIO\_パス\_正常性\_情報 WMI クラス


WMI クライアントは、mpio\_PATH\_HEALTH\_INFO WMI クラスを使用して、mpio によって管理されるすべてのパスの統計情報を収集するように MPIO に照会します。

```cpp
class MPIO_PATH_HEALTH_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    [WmiDataId(1),
     read,
     Description("Number of Path Health Packets.") : amended
    ] uint32 NumberPathPackets;

    [WmiDataId(2),
     read,
     Description("Reserved for future use.") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     Description("MPIO Path Health Info Array.") : amended,
     WmiSizeIs("NumberPathPackets")
    ] MPIO_PATH_HEALTH_CLASS PathHealthPackets[];
};
```

WMI ツールでクラス定義をコンパイルすると、 [**MPIO\_PATH\_HEALTH\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_path_health_info)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





