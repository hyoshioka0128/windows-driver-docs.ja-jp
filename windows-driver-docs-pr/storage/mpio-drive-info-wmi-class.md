---
title: MPIO\_ドライブ\_情報 WMI クラス
description: MPIO\_ドライブ\_情報 WMI クラス
ms.assetid: 4c116157-5f5b-4213-abdd-9128ebbfa341
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7631991eb53566830951fc83c480b19c3de7afb9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844973"
---
# <a name="mpio_drive_info-wmi-class"></a>MPIO\_ドライブ\_情報 WMI クラス


Mpio ドライバーは、MPIO\_DRIVE\_INFO WMI クラスを使用して、管理対象のシステム上の各 MPIO ディスクを識別します。

```cpp
class MPIO_DRIVE_INFO
{
    //
    // Number of Paths to the real device.
    //
    [WmiDataId(1)] uint32 NumberPaths;

    //
    // The MPIODisk(N).
    //
    [WmiDataId(2), MaxLen(63)] string Name;

    //
    // The real device's serial number.
    //
    [WmiDataId(3), MaxLen(63)] string SerialNumber;

    //
    // Friendly name of the DSM controlling the device.
    //
    [WmiDataId(4), MaxLen(63)] string DsmName;
};
```

このクラス定義が WMI ツールスイートによってコンパイルされると、 [**MPIO\_DRIVE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_drive_info)データ構造が生成されます。 この WMI クラスに関連付けられているメソッドはありません。

 

 





