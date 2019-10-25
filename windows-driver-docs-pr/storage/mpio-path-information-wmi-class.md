---
title: MPIO\_パス\_情報 WMI クラス
description: MPIO\_パス\_情報 WMI クラス
ms.assetid: fd6311c5-2d98-4a3a-beb9-54f3a84be8eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0b082bfb08f63eeaaf4631653f92e668389420a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844959"
---
# <a name="mpio_path_information-wmi-class"></a>MPIO\_パス\_情報 WMI クラス


WMI クライアントは、mpio\_PATH\_INFORMATION WMI クラスを使用して、mpio ディスクに関連付けられているすべてのパスに関する情報を MPIO ドライバーに照会します。

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

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_パス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_path_information)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





