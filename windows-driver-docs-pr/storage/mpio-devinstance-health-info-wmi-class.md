---
title: MPIO\_DEVINSTANCE\_HEALTH\_INFO WMI クラス
description: MPIO\_DEVINSTANCE\_HEALTH\_INFO WMI クラス
ms.assetid: 4d47b41b-eac6-4f8b-801b-76eec8158074
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b1db90c4297cf84541920141eebd7fba158c4c68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844551"
---
# <a name="mpio_devinstance_health_info-wmi-class"></a>MPIO\_DEVINSTANCE\_HEALTH\_INFO WMI クラス


Mpio ドライバーは、MPIO\_DEVINSTANCE\_HEALTH\_INFO WMI クラスを使用して、基になるさまざまなパスを使用して、MPIO ディスクの正常性の統計情報をレポートします。

```cpp
class MPIO_DEVINSTANCE_HEALTH_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    [WmiDataId(1),
     read,
     Description("Number of Health Packets.") : amended
    ] uint32 NumberDevInstancePackets;

    [WmiDataId(2),
     read,
     Description("Reserved for future use.") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     Description("Multi-Path Health Info Array.") : amended,
     WmiSizeIs("NumberDevInstancePackets")
    ] MPIO_DEVINSTANCE_HEALTH_CLASS DevInstanceHealthPackets[];
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_DEVINSTANCE\_HEALTH\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_devinstance_health_info)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





