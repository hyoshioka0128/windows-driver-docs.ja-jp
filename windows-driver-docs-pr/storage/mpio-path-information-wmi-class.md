---
title: MPIO\_パス\_情報 WMI クラス
description: MPIO\_パス\_情報 WMI クラス
ms.assetid: fd6311c5-2d98-4a3a-beb9-54f3a84be8eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 74908b3bd56cdd4516584a02e726136fffd4322e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536057"
---
# <a name="mpiopathinformation-wmi-class"></a>MPIO\_パス\_情報 WMI クラス


WMI クライアントが、MPIO を使用して\_パス\_を MPIO ドライバーについては、MPIO ディスクに関連付けられているすべてのパスに関する情報の WMI クラスです。

```cpp
class MPIO_PATH_INFORMATION
{

    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Number of paths to the device.
    //
    [WmiDataId(1),
     read,
     Description("Number of Paths in use") : amended
    ] uint32 NumberPaths;

    //
    // Pad for data alignment.
    //
    [WmiDataId(2),
     read,
     Description("Pad for ULONGLONG Alignment.") : amended
    ] uint32 Pad;

    //
    // Array containing each path&#39;s information.
    // Note that each of these are ULONGLONG aligned.
    //
    [WmiDataId(3),
     read,
     Description("Array of Adapter/Path Information.") : amended,
     WmiSizeIs("NumberPaths")
    ] MPIO_ADAPTER_INFORMATION PathList[];

};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_パス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff562441)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





