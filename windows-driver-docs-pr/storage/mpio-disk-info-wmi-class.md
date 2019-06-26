---
title: MPIO\_ディスク\_情報 WMI クラス
description: MPIO\_ディスク\_情報 WMI クラス
ms.assetid: 75c66c84-d815-43a5-a70d-1952bf0e8d44
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cba52b3b14290427d84f6893bf2b9fe7d4d51bb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386162"
---
# <a name="mpiodiskinfo-wmi-class"></a>MPIO\_ディスク\_情報 WMI クラス


WMI クライアントが、MPIO を使用して\_ディスク\_MPIO はすべて MPIO に関する情報を収集できるようにディスクをクエリする情報の WMI クラスは、システムで構成されます。

```cpp
class MPIO_DISK_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // The Number of multi-path disk pdos that have been
    // created.
    //
    [WmiDataId(1),
     read,
     Description("Number of Multi-Path Drives.") : amended
    ] uint32 NumberDrives;

    //
    // Variable-length array of DRIVE_INFO structures.
    // NOTE: Each entry will be ULONG aligned. App. writers
    // take note when iterating through the array.
    //
    [WmiDataId(2),
     read,
     Description("Multi-Path Drive Info Array.") : amended,
     WmiSizeIs("NumberDrives")
    ] MPIO_DRIVE_INFO DriveInfo[];
};
```

WMI ツール スイートによってコンパイルされると、このクラスの定義を生成、 [ **MPIO\_ディスク\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_disk_info)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





