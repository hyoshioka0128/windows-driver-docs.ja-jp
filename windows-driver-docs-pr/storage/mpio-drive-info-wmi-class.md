---
title: MPIO\_ドライブ\_情報 WMI クラス
description: MPIO\_ドライブ\_情報 WMI クラス
ms.assetid: 4c116157-5f5b-4213-abdd-9128ebbfa341
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 535686b0e2f5bed53a433fc6d9c8337e6c3ba5eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386157"
---
# <a name="mpiodriveinfo-wmi-class"></a>MPIO\_ドライブ\_情報 WMI クラス


MPIO ドライバーは、MPIO を使用して\_ドライブ\_管理しているシステム上の各 MPIO ディスクを識別する情報の WMI クラスです。

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

このクラスの定義が WMI ツール スイートによってコンパイルされると、生成、 [ **MPIO\_ドライブ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_drive_info)データ構造体。 この WMI クラスに関連付けられているメソッドはありません。

 

 





