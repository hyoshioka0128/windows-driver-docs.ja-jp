---
title: MPIO\_パス\_情報 WMI クラス
description: MPIO\_パス\_情報 WMI クラス
ms.assetid: fd6311c5-2d98-4a3a-beb9-54f3a84be8eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e89093533c2a15f215d787e97fc0d91e983670ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386147"
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
    // Array containing each path's information.
    // Note that each of these are ULONGLONG aligned.
    //
    [WmiDataId(3),
     read,
     Description("Array of Adapter/Path Information.") : amended,
     WmiSizeIs("NumberPaths")
    ] MPIO_ADAPTER_INFORMATION PathList[];

};
```

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_パス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_path_information)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





