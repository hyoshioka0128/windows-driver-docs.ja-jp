---
title: MPIO\_パス\_ヘルス\_情報 WMI クラス
description: MPIO\_パス\_ヘルス\_情報 WMI クラス
ms.assetid: 26c329d0-0d9c-4d24-bbe4-ebb7d7b36a89
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cff2fa5b9c4476b8e7fe21b552503dcdd9545093
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570123"
---
# <a name="mpiopathhealthinfo-wmi-class"></a>MPIO\_パス\_ヘルス\_情報 WMI クラス


WMI クライアントが、MPIO を使用して\_パス\_ヘルス\_MPIO によって管理されているすべてのパスの統計情報を収集するために MPIO を照会する情報の WMI クラスです。

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

WMI ツールの suiteit によって、クラス定義をコンパイルするときに生成、 [ **MPIO\_パス\_ヘルス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562431)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





